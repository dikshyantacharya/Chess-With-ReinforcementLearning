# opencampus-chess
### A Chess-AI Project for "Machine Learning with Tensorflow"

---

## Overview
This project focuses on developing a Chess AI using TensorFlow within the scope of a machine learning course. It includes three Jupyter Notebooks and two datasets integral to the AI's training and evaluation.

---

## Contents
### Powerpoint Presentation
`Power-Point Presentation.pptx` contains the presentation that was done during the final project

### Jupyter Notebooks
1. **checkmate_generator.ipynb**
   - *Purpose*: Generates datasets in CSV format with final chessboard positions and labels (0 for draw, 1 for white's checkmate, -1 for black's checkmate).
   - *Datasets Generated*:
     - `1-200000_game.zip`: Zipped to meet GitHub's file size constraints.
     - `1-model_200000_game_stat.csv`: Provides statistical analysis of games played during the dataset generation.

   This notebook simulates chess games played against itself, recording the final positions and outcomes. The dataset is balanced to ensure an equal proportion of wins, losses, and draws.

2. **checkmate_trainer.ipynb**
   - *Purpose*: Trains a CNN model using the dataset from `checkmate_generator.ipynb`.
   - *Highlights*: Includes model evaluation and testing, demonstrating correct and incorrect model predictions.

3. **reinforcement_trainer.ipynb**
   - *Purpose*: Records the entire sequence of board positions from start to end for each game.
   - *Challenge*: High computational demand limited the generation of a substantial training dataset. So, the model with reinforcement learning could not be implemented.

---

## Challenges and Future Directions
- **Dataset Generation**: The high computational demand for evaluating board positions posed a significant challenge in generating a comprehensive dataset.
- **Future Improvements**:
  - Implement parallel processing for accelerated dataset generation.
  - Simplify the CNN model to reduce computational requirements while maintaining accuracy.

---

Contributions and suggestions for project improvement are highly welcomed!
