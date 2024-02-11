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

## Introduction
This project presents a simple reinforcement learning model designed to play chess. The model is encapsulated within a Jupyter Notebook named "reinforcement learning model creator," leveraging a Convolutional Neural Network (CNN) to interpret chessboard positions and predict game moves.

## Project Overview
The core idea is to translate a chessboard position into a multidimensional array, assigning each square an encoded vector representing the piece it contains, castling rights, and the turn (either White or Black). This results in an 8x8 board with each square detailed in a 17-dimension one-hot encoding format, making up the input for the CNN.

### Components
- **Board Representation**: Transforms board positions into a multidimensional array (8x8x17), encoding piece information, castling rights, and turn data.
- **Convolutional Neural Network**: Processes the encoded board positions to output a policy vector and a value estimation:
  - **Policy Output**: A probability distribution over 4672 possible chess moves, adjusted to discount invalid moves and normalize valid ones.
  - **Value Output**: An evaluation of the current board position, indicating the winning odds for the active side.

### Methodology
- **Data Generation**: The model uses the policy output for data generation through a balance of exploration and exploitation, dynamically adjusting move selection based on the predicted value of each position.
- **Move Selection**: Employs a strategy where 85% of moves are chosen based on the highest probability (exploitation), and 15% are selected at random (exploration) to diversify gameplay and learning.
- **Value Function**: Determines the value of a board position at the end of the game, influenced by the game outcome (win, loss, draw) and modified by piece strength in draw scenarios. The value of each preceding move is adjusted to reflect its contribution to the final outcome, using a discount factor for temporal credit assignment.

### Experimentation and Results
After training on 100 simulated games, the model was tested against an opponent making random moves. Observations revealed the model had learned basic strategies, such as piece capture and pawn promotion, without explicit programming for these behaviors. However, it struggled to achieve checkmate, likely due to a lack of training data featuring checkmate scenarios.

### Challenges and Future Directions
- **Enhanced Training Data**: Generating additional game data with a focus on checkmate situations could significantly improve model performance.
- **Monte Carlo Tree Search**: Implementing a deeper lookahead strategy could offer more strategic depth in move selection.
- **Policy Network Refinement**: Adjusting the policy network to favor moves leading to higher value outcomes may enhance the model's strategic capabilities.

## Getting Started
To explore and utilize this reinforcement learning model for chess, follow the steps outlined below:

### Prerequisites
- Jupyter Notebook
- Python 3.x
- Libraries: NumPy, TensorFlow, Keras

### Installation
1. Clone the project repository.
2. Install the required libraries using `pip install numpy tensorflow keras`.
3. Launch the Jupyter Notebook `reinforcement learning model creator.ipynb` to begin experimenting with the model.

## Conclusion
This project represents an initial foray into applying simple reinforcement learning techniques to the complex game of chess. Despite its preliminary nature, the model demonstrates promising capabilities in learning basic chess strategies. Continued development and refinement are expected to enhance its performance, particularly in achieving checkmate, the ultimate goal in chess.


Contributions and suggestions for project improvement are highly welcomed!
