# opencampus-chess
### A Chess-AI Project for "Machine Learning with Tensorflow"

---

## Overview
This project focuses on developing a Chess AI using TensorFlow as part of a machine learning course. It comprises three Jupyter Notebooks (one of which is hosted on Google Colab, with the link provided below) and one dataset that is essential for the AI's training and evaluation. The checkmate_generator.ipynb and checkmate_trainer.ipynb are experimental models to explore whether the representation of the chessboard can be trained into a neural network to make desired moves. This approach proved to be successful. Consequently, a simple AI, initially lacking any knowledge of chess, is trained using Deep Reinforcement Learning. Through this process, it learns some key aspects of the game, such as the importance of piece capture, pawn movement, etc.

---

## Sources
For the conversion of the chess representation. I took the idea from "[Geohot twitchchess](https://github.com/geohot/twitchchess/blob/master/state.py)" projekt. And for the idea of applying simple Deep Reinfrocement Learning, the core idea like PolicyNetwork, ValueNetwork, conversion of policy network idex to move was implemeted from the [project](https://github.com/zjeffer/chess-deep-rl)

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
This project is done on Google Colab and can be accessed [here](https://colab.research.google.com/drive/1Ga5Dh5zpevrn3l301Mh45pHvEUCI_r-w?usp=sharing#scrollTo=3guW_3NLrNoU). At the end, there's a demonstration of gameplay using the model developed, so registration in Colab is necessary to view the full game. All methods are thoroughly commented to provide clear understanding. Read the description below for insights into why and how the concepts were implemented.


## Introduction

This project is an exploration into applying reinforcement learning to the game of chess. The core of the project is encapsulated in a Jupyter Notebook titled "reinforcement learning model creator," which outlines the development and testing of a convolutional neural network (CNN) based model designed to understand and make decisions in chess.

## Project Description

The project begins with the challenge of representing a chessboard in a format suitable for machine learning. The solution involves converting the board position into a multidimensional array. Each square on the board is represented by a vector of length 17, encoding the piece present, the castling rights, and whose turn it is, resulting in an 8x8 board representation where each square is detailed in this 17-dimension one-hot encoding format.

### Convolutional Neural Network (CNN)

The CNN takes this board representation as input and produces two outputs:
- **Policy**: A probability distribution over the possible actions in a chess game.
- **Value**: An estimation of the winning chances for the current player.

The policy output is based on the concept that there are 4672 possible types of chess moves, a figure that comes from considering the specifics of the current square, the destination square's distance and direction, and the type of piece making the move. This is mentioned in the [thesis](https://github.com/zjeffer/howest-thesis) where the author uses the idea implemeted during creation of Alphazero. This comprehensive approach to move generation ensures the model considers a wide array of possible moves, which are then pruned and normalized to ensure only valid moves are considered.

### Data Generation and Move Selection

Data generation for training the model utilizes a balance between exploration and exploitation. For 85% of the time, the model selects the move with the highest probability, encouraging the model to make the most sensible move based on its current knowledge. The remaining 15% of the time, the model selects a move at random, allowing for the exploration of new, potentially superior strategies. This methodology ensures that the model not only reinforces its existing strategies but also discovers new and possibly more effective ones. Initially, the exploitation-exploration ratio was set at approximately 95%-5%. In this configuration, the games tended to repeat due to insufficient exploration. Therefore, the exploration rate was increased to determine at what point the model would stop repeating games while still leading to similar positions. It was observed that an 85%-15% exploitation-exploration ratio achieved this balance.

### Value Function

The value function assigns a score to the board positions at the end of the game. The scoring is as follows:
- **0** for a draw,
- **-1** for a loss for White,
- **+1** for a win for White,
- **+0.25** if the game is drawn but White has a material advantage of +5,
- **-0.25** if the game is drawn but Black has a material advantage of -5.

These scores are then adjusted using a discount factor to reflect the value of positions leading up to the game's conclusion, ensuring that each move's value reflects its contribution to the overall game outcome. For example, if White wins the game, the final board position is assigned a value of +1. This value decreases with each preceding move, so that by the time it reaches the starting position, it approaches 0 (but retains a slightly positive value). The same principle is applied from Black's perspective. If a game ends in a draw, all moves leading to that position are marked as such.

### Training and Evaluation

After training on 50 simulated games (about 3000 chess position), the model was trained and then tested against a player making random moves. The results indicated that the model had learned basic strategies such as capturing pieces and promoting pawns without being explicitly programmed to do so. However, the model struggled to achieve checkmate, primarily due to the training data being heavily skewed towards draw outcomes rather than decisive victories or losses. So, it simply made repetative move after the capture of the pieces. 

### Hyper Paramater tuning
The model was tested with various learning rates, batch sizes, and epochs, but these changes did not significantly affect the results. Consequently, an epoch of 10 was selected, with a learning rate of 1e-3 and a batch size of 3. The main factor that influenced the game's outcome was the number of positions available in the datasets, as well as the layers of the Convolutional Neural Network (CNN). A compromise had to be made regarding the CNN's filters. Increasing the number of filters improved the accuracy of the policy, but it also required more time to compute each board position to complete a game. Therefore, a choice was made to ensure the model could learn effectively while remaining computationally efficient. CNN was chosen because it demonstrated strong performance during the testing of the checkmate-trainer.

### Evaluation
The training data were plotted to visualize the learning curves for both the policy and evaluation functions. Predicting the policy proved challenging because it required forecasting 4672 probabilities for a single board position, resulting in accuracy rates consistently near 0 for both the training and testing sets. However, the mean squared error (MSE) for the value of chess positions was satisfactory. This was evident during the final gameplay against an opponent making random moves, where the model's evaluation of positions demonstrated good accuracy.

### Observations and Future Work

The testing phase revealed that while the model had learned to capitalize on capturing opportunities and pawn promotion, it lacked the strategic depth to consistently deliver checkmate. This was attributed to the predominance of drawn positions in the training data. Future improvements could include incorporating a Monte Carlo Tree Search for deeper strategic planning and refining the policy network to prioritize high-value moves more effectively.

### Bug in project
A bug was identified where, very rarely, a move is mapped beyond the scope of available moves. Debugging this error has not yet been undertaken due to its difficulty in replication, occurring approximately once in every 200 games played. This issue will be addressed and rectified in upcoming improvements.

## Conclusion

This project represents an initial step towards creating a chess-playing AI through reinforcement learning. Despite the model's current limitations, it demonstrates promising capabilities in learning and applying basic chess strategies. Continued development, focused on enhancing the model's exposure to a variety of game outcomes and strategic depth, will be crucial in overcoming the current challenges and achieving a more competitive level of play.

## Submission Details

- **Submitted By:** Dikshyant Acharya
- **Submitted On:** 2024-02-11
- **Submitted To:** Florian Schlösser

Contributions and suggestions for project improvement are highly welcomed!
