# opencampus-chess
A Chess-AI Project done for course "Machine Learning with Tensorflow"
Overview

This project focuses on developing a Chess AI using machine learning techniques. It comprises three Jupyter Notebook files and two datasets, which are integral to the functioning and training of the AI model.
File Descriptions

    checkmate_generator.ipynb:
        Functionality: Generates datasets in CSV format.
        Data: Final positions on a chessboard with labels (0 for draw, 1 for white's checkmate, -1 for black's checkmate).
        Output Files:
            1-200000_game.zip: Contains the generated data (zipped due to GitHub's file size limitations).
            1-model_200000_game_stat.csv: Statistical analysis of each game played during dataset generation.

    This notebook simulates chess games played against itself, capturing the final board positions and outcomes. After simulating 200,000 games, the data is balanced to ensure an equal proportion of wins, losses, and draws.

    checkmate_trainer.ipynb:
        Functionality: Trains a Convolutional Neural Network (CNN) model using the dataset from checkmate_generator.ipynb.
        Highlights: The notebook includes model evaluation and testing, showcasing both correct and incorrect model predictions.

    reinforcement_trainer.ipynb:
        Functionality: Unlike checkmate_generator, this notebook records the entire sequence of board positions from the start to the end of each game.
        Process: The model is intermittently trained after every 10 games using these sequences.

    However, due to the extensive computational demand (each game requiring the evaluation of approximately 9,000 board positions for a single move prediction), the dataset for effective training could not be generated with the available computational resources.

Future Improvements

To enhance this project:

    Parallel Processing: Implement parallel game simulations to speed up dataset generation.
    Model Optimization: Simplify the CNN model to reduce computational load without significantly compromising prediction accuracy.
