# Chess Engine: Deep Neural Network vs Bayesian Neural Network #

This repository contains the implementation of a chess engine that utilizes two different models: a Deep Neural Network (DNN) and a Bayesian Neural Network (BNN). The goal of this project is to compare the performance of these models in a regression setting, where they are used as evaluator functions in an integrated system of decision making.

## Model Architecture ##

Both models follow a similar structure and consist of 10 layers. The input layer takes a custom binary representation of the chess board, encoded in a vector of length 896. Each subsequent layer has 896 neurons. The output layer provides the evaluation of the engine, which is clipped within the range of -15 to +15.

The DNN model uses Rectified Linear Unit (ReLU) as the nonlinearity function in its layers. On the other hand, the BNN model is tested with multiple activation functions to determine the most suitable one for modeling uncertainty.

## Loss Functions ##

For the DNN model, the mean element-wise absolute value difference (L1 loss) is used as the loss metric, as it is measured in the same units as the evaluation values. The BNN model combines L1 loss with Kullback-Leibler (KL) divergence to account for the Bayesian version. The weights of each node are adjusted using the following formula:

$θ^* = L1 [P(w|X, Y)] - KL [P(w|X, Y)]$

## Data Management ##

The data used for this experiment is sourced from Lichess, an online chess platform with millions of recorded games. The data is obtained with the consent of the subscribers upon registration, and there are no legal issues associated with its collection.

The data is stored in an interactive SQL database with 3 million entries. Each entry contains the position ID, Forsyth–Edwards Notation (FEN) interpretation of the board, and Stockfish evaluation. FEN notation encodes the board position in an alphanumeric format, providing a detailed representation of the board state.

To ensure compatibility with neural networks, the board representation is transformed into a three-dimensional matrix of dimensions (14, 8, 8). This representation includes 12 boards for the individual pieces and an additional two boards for representing the attacked squares of each player. The resulting matrix is compressed into a 896-vector, which serves as the final input for the models.

The evaluation values (Y) of the dataset represent the board evaluations and are clipped within the range of -15 to +15. These values indicate the advantage/disadvantage of a player, with negative values favoring black and positive values favoring white.

## Engine Decision Making Process ##

The neural network models are integrated into an agent-based environment using a decision tree. The decision tree represents possible outcomes as nodes, and moves as branches leading to those nodes. The root of the tree represents the present state of the board, and the algorithm traverses the tree by calling the evaluator for a given depth of iterations.

The decision-making process follows the principles of the minimax algorithm, assuming perfect play from the opponent. The algorithm alternates between maximizing and minimizing the values of the nodes, with the goal of avoiding undesirable outcomes. Alpha-beta pruning is employed to optimize the search process and avoid extensive calculations.

## Testing Methods ##

The testing methodology involves evaluating the performance of the models in a game setting format, where agents utilizing the evaluation functions derived from the neural networks compete against each other. The evaluation metric focuses on the raw streak of wins and losses, providing a pragmatic measure of performance.

Additionally, the L1 loss metric is employed to compare the performance of both engines on common grounds. By using the same loss metric, a favorable comparison for the deterministic approach is expected.

Before comparing the models, the BNN (Bayesian Neural Network) are trained with different sets of priors, and the set that yields the smallest loss will be selected. Then, using those priors, the BNN will be tested with different types of activation functions to determine which one works better with the Bayesian model.

## Conclusions ##

The game of chess has fascinated thinkers for centuries, and in the modern era, machines have taken the lead in exploring adaptive systems. This paper combines probabilistic thinking with deterministic environments, yielding promising results and inspiring future discussions. The integration of a Bayesian framework into adaptive systems is a significant contribution, bridging the gap between the game of chess and statistical theory. By leveraging deep neural networks and comparing them with Bayesian neural networks, this study sheds light on modeling uncertainty. These findings motivate further exploration and collaboration across the fields of statistics, computer science, and game theory, inspiring researchers to push the boundaries of knowledge.

