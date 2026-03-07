# PowerPINN Notebook Guide

## Introduction
`PINN.ipynb` is the main training notebook for a **Physics-Informed Neural Network (PINN)** built on the IEEE 14-bus power system.

The notebook combines:
- **Data-driven learning** (fit predicted voltage magnitude/angle to labeled states), and
- **Physics constraints** (power-balance consistency from the admittance matrix `Y_bus`).

In short, the model learns grid state estimation from measurements while being penalized when predictions violate power-system physics.

## Neural Network Architecture and Training Data
- Inputs are 28 features per scenario: first 14 are active power-related terms (`P`), last 14 are reactive power-related terms (`Q`).
- Outputs are 28 state values: 14 voltage magnitudes and 14 voltage angles.
- The training dataset is loaded from `ieee14_training_data.pt`.

## Notebook structure (`PINN.ipynb`)
1. **Environment setup**: installs required packages from `requirements.txt`.
2. **Initialization**: loads IEEE 14-bus model, inspects grid tables, loads training data, extracts `Y_bus`.
3. **Model + losses**:
	- `PowerPINN` neural network
	- `physics_loss(...)` enforcing power consistency
4. **Training**: optimizes weighted data loss + physics loss.
5. **Visualization**: plots training data snapshots and loss curves.
6. **Save model**: writes `pinn_model.pth` for later evaluation.

## Quick run order
Run cells top-to-bottom.

Minimum required local files:
- `PINN.ipynb`
- `requirements.txt`
- `ieee14_training_data.pt`

## Next Steps
Simulate an FDIA to evaluate the model and compare against WLS.
