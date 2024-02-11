# opencampus-chess
### A Chess-AI Project for "Machine Learning with Tensorflow"

---

## Overview
This project focuses on developing a Chess AI using TensorFlow within the scope of a machine learning course. It includes three Jupyter Notebooks (1 is in google cola, link is mentioned below) and 1 dataset integral to the AI's training and evaluation. The checkmate_generator.ipynb and checkmate_trainer.ipynb is a tryout models to see, if the representation of the board can be tranied into neural network  to make desire move . This turned out to be ture, so a simple AI having initially 0 knowledge of chess is trained using Deep Reinforcement Learning where it learns some key component of game, like importance of piece capture, pawn movement etc.

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
This is done in Google Colab and can be accessed [here](https://colab.research.google.com/drive/1Ga5Dh5zpevrn3l301Mh45pHvEUCI_r-w?usp=sharing#scrollTo=3guW_3NLrNoU). At the end, there is a game play using the model created, so registration in Colab is required, to view the full game played. All the methods are thoroughly commented. Read below description to have an insight, why and how the concepts are being implemented. 

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

Data generation for training the model utilizes a balance between exploration and exploitation. For 85% of the time, the model selects the move with the highest probability, encouraging the model to make the most sensible move based on its current knowledge. The remaining 15% of the time, the model selects a move at random, allowing for the exploration of new, potentially superior strategies. This methodology ensures that the model not only reinforces its existing strategies but also discovers new and possibly more effective ones.

### Value Function

The value function assigns a score to the board positions at the end of the game. The scoring is as follows:
- **0** for a draw,
- **-1** for a loss for White,
- **+1** for a win for White,
- **+0.25** if the game is drawn but White has a material advantage of +5,
- **-0.25** if the game is drawn but Black has a material advantage of -5.

These scores are then adjusted using a discount factor to reflect the value of positions leading up to the game's conclusion, ensuring that each move's value reflects its contribution to the overall game outcome. For instance, if white has won the game, then the final board position will have value of +1 and it decreases with each preceeding move such that when it reaches to the start of the position, it finally reaches near 0 (but have slightly positive valve). Same is applied from blacks perspective. If a game is drawn, all the move leading to that position is maked as drawn.

### Training and Evaluation

After training on 50 simulated games, the model was trained and then tested against a player making random moves. The results indicated that the model had learned basic strategies such as capturing pieces and promoting pawns without being explicitly programmed to do so. However, the model struggled to achieve checkmate, primarily due to the training data being heavily skewed towards draw outcomes rather than decisive victories or losses. So, it simply made repetative move after the capture of the pieces. 

### Hyper Paramater tuning
The model was tried with different learning rate, batch sizes, epochs. But it didnt change the result significantly. The main factor that influeced the outcome of game was number of position, that it had in datasets, and also the layers of CNN. A trade-off was being made for the Filters of CNN. When using more CNN filter, it was able to increase the accuracy of policy, but it took more time to compute every board position to finish a game. So, it was choosen, sucht that the model is able to learn something, and still being computationally efficient. CNN was choosen, since it performed well during testing of the checkmate-trainer.

### Evaluation
The trained data were plotted where the policy and evaluation learning can be seen. The prediction of policy was difficult, since 4672 probablities needs to be predicted for a single board position. So, the accuracy was always near 0 for both training and testing set. 
### Observations and Future Work

The testing phase revealed that while the model had learned to capitalize on capturing opportunities and pawn promotion, it lacked the strategic depth to consistently deliver checkmate. This was attributed to the predominance of drawn positions in the training data. Future improvements could include incorporating a Monte Carlo Tree Search for deeper strategic planning and refining the policy network to prioritize high-value moves more effectively.

## Conclusion

This project represents an initial step towards creating a chess-playing AI through reinforcement learning. Despite the model's current limitations, it demonstrates promising capabilities in learning and applying basic chess strategies. Continued development, focused on enhancing the model's exposure to a variety of game outcomes and strategic depth, will be crucial in overcoming the current challenges and achieving a more competitive level of play.


Contributions and suggestions for project improvement are highly welcomed!
