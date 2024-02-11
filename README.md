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

# Simple Reinforcement Learning Model for Chess

This project aims to develop a reinforcement learning model for playing chess. The model is built using a Convolutional Neural Network (CNN) that processes chessboard positions and outputs policy and value predictions to guide decision-making during a game.

## Overview

The reinforcement learning model operates on a multi-dimensional array representation of the chessboard. Each square on the board is encoded into a 17-dimensional vector using one-hot encoding to represent the piece on the square, castling rights, and the player's turn. This results in an 8x8x17 input tensor for the CNN.

### Model Components

- **Board Representation**: The chessboard is converted into a multi-dimensional array where each square is described by a 17-dimensional vector.
- **Convolutional Neural Network**: Takes the board position as input and outputs a policy and value.
  - **Policy**: A distribution over 4672 possible chess moves, based on the current square, move distance, direction, and piece type.
  - **Value**: Indicates the winning chances for each side from the current board position.

### Model Logic

1. **Data Generation**: Utilizes the policy output for exploration vs. exploitation, generating game data.
2. **Move Selection**: Employs an 85-15 rule for choosing moves based on their probability to balance between exploiting known strategies and exploring new positions.
3. **Value Function**: Assigns values to game outcomes (win, loss, draw) and distributes these values back through the move sequence, adjusting for piece strength in drawn positions.

### Training and Evaluation

The model was trained on 100 game simulations and then evaluated by playing against a baseline opponent making random moves. Initial observations showed the model learned basic strategies like piece capture and pawn promotion but struggled with achieving checkmate due to a lack of training data featuring checkmate outcomes.

### Future Directions

Improvements could include:
- Generating more diverse training data with a higher incidence of checkmate.
- Integrating a Monte Carlo Tree Search for deeper lookahead.
- Refining the policy network to prioritize moves leading to higher value outcomes.

## Getting Started

### Prerequisites

- Python 3.x
- Jupyter Notebook
- Required Python libraries: `numpy`, `tensorflow`, `keras`

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>


Contributions and suggestions for project improvement are highly welcomed!
