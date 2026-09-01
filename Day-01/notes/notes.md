# Day 01 — BioHub Problem & Evaluation Metrics

**Phase:** 01 — Biology & Problem Understanding  
**Learning Day:** 01  
**Topic:** BioHub problem, detection, tracking and evaluation

## Learning Goal

Understand what BioHub is trying to solve and how cell detection, tracking, cell division and lineage are evaluated.

## 1. Cell Detection

The first task is to determine where cells are present in microscopy images.

- **True Positive (TP):** A cell exists and the model predicts a cell.
- **False Positive (FP):** The model predicts a cell, but no cell exists.
- **False Negative (FN):** A real cell exists, but the model fails to detect it.
- **True Negative (TN):** No cell exists and the model correctly predicts no cell.

### Precision

Precision asks:

> Of the cells predicted by the model, how many were actually cells?

**Precision = TP / (TP + FP)**

High precision means fewer false cell detections.

### Recall

Recall asks:

> Of all real cells, how many did the model find?

**Recall = TP / (TP + FN)**

High recall means fewer cells were missed.

### F1-Score

F1 combines precision and recall.

**F1 = 2 × (Precision × Recall) / (Precision + Recall)**

F1 is high when both precision and recall are reasonably high.

## 2. IoU — Intersection over Union

IoU measures how much a predicted cell region overlaps with the true cell region.

**IoU = Intersection / Union**

- Intersection = area shared by prediction and ground truth.
- Union = total area covered by either prediction or ground truth.

## 3. Cell Tracking

Detection alone is not enough for BioHub.

The system must follow cells through time and determine whether a cell in one frame corresponds to the same cell in another frame.

### Identity Switch

An identity switch occurs when the tracking system accidentally changes the identity assigned to a cell.

Example:

Frame 1: A, B  
Frame 2: B, A

The cells may be detected at the correct positions, but their identities have been switched.

## 4. Cell Division and Lineage

Cells can divide during development.

Example:

A → B  
A → C

Here, A is the parent and B and C are daughter cells.

Following these parent → daughter relationships is part of **lineage reconstruction**.

## 5. BioHub as a Graph

BioHub can be understood as a cell graph:

- **Node** = a cell
- **Edge** = a connection between cells across time
- **Division** = a parent cell connected to two or more daughter cells

Conceptually:

BioHub
→ Detection
→ Tracking
→ Cell Division
→ Lineage Tracking
→ Parent → Daughter relationships

## 6. BioHub Evaluation

BioHub evaluates more than simple cell detection.

### Adjusted Edge Jaccard

Measures how correctly the model reconstructs cell-to-cell connections.

Predicted cells are first matched to ground-truth cells using their spatial positions. The competition uses physical distance and a maximum matching distance of **7 µm**.

The physical voxel scale is:

- z = 1.625 µm/voxel
- y = 0.40625 µm/voxel
- x = 0.40625 µm/voxel

The matched nodes are then used to compare predicted and ground-truth edges.

### Division Jaccard

Measures how correctly the model identifies cell division relationships.

A node with two or more outgoing edges represents a division event.

### BioHub Score

**Final Score = Adjusted Edge Jaccard + 0.1 × Division Jaccard**

Therefore, BioHub is not only about finding cells. It is about correctly reconstructing how cells move, connect through time and divide.

## Key Takeaways

- Precision → how many predicted cells are correct.
- Recall → how many real cells were found.
- F1 → combines precision and recall.
- IoU → measures region overlap.
- Node → cell.
- Edge → connection between cells across time.
- Identity switch → cell identity is incorrectly changed.
- Cell division → one parent produces daughter cells.
- Lineage → parent → daughter relationships.
- Adjusted Edge Jaccard → evaluates cell connections.
- Division Jaccard → evaluates cell divisions.

## Day 01 Self-Test

- Precision calculation understood ✓
- Recall calculation understood ✓
- Identity switches understood ✓
- Nodes and edges understood ✓
- Cell division and lineage understood ✓
- BioHub evaluation metrics understood ✓
