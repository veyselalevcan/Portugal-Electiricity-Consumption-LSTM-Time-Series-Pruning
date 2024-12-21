# Portugal-Electiricity-Consumption-LSTM-Time-Series-Pruning

Forecasting Electricity Consumption with LSTM Models: A Comparative Analysis with Pruning

Introduction

Electricity consumption forecasting plays a critical role in energy management and policy-making. With advancements in machine learning, time series models such as Long Short-Term Memory (LSTM) networks have become increasingly popular due to their ability to capture temporal dependencies. In this paper, we discuss the use of LSTM models to forecast electricity consumption in Portugal, incorporating model pruning to improve efficiency. The methodology, experiments, and results are analyzed, with a focus on the impact of pruning on performance metrics and computational efficiency.

Methodology

Data Preprocessing

Electricity consumption data from the ENTSO-E Transparency platform was used. Key preprocessing steps included:

Filtering and Cleaning: Data columns were reduced to focus on electricity consumption values for Portugal.

Scaling: A MinMaxScaler normalized the data to values between 0 and 1 for compatibility with the LSTM activation functions.

Sequence Creation: Input sequences of 24 hours (one day) were generated to capture daily patterns.

LSTM Architecture

An initial, non-pruned LSTM model was developed with the following features:

Units: 50 units were used to balance model complexity and computational efficiency.

Activation Function: The ReLU activation was chosen for its simplicity and computational advantages, avoiding vanishing gradient problems common with sigmoid and tanh.

Output: A single dense layer output was used to predict the next time step in the series.

The LSTM's recurrent nature enables it to handle dependencies across time steps. The choice of 50 units was empirically validated to offer a good trade-off between accuracy and computational load for this dataset.

Model Training and Evaluation

Both pruned and non-pruned models were trained on 80% of the data and tested on the remaining 20%. The models were optimized using the Adam optimizer and mean squared error (MSE) loss function.

Metrics Used

Mean Squared Error (MSE): Measures the average squared difference between predicted and actual values.

Mean Absolute Error (MAE): Quantifies the average absolute difference, providing a more interpretable measure of prediction accuracy.

Model Pruning

Model pruning involves reducing the number of weights in the LSTM network to enhance efficiency. Pruning parameters included:

Initial Sparsity: 20%

Final Sparsity: 80%

Pruning Schedule: Polynomial decay from the beginning to 1,000 training steps.

Pruned weights were stripped of pruning wrappers for final evaluations.

Experimental Results

Non-Pruned Model Performance

The non-pruned model achieved the following metrics:

MSE: 15.28

MAE: 3.84

Visualization of predictions revealed that the model captured daily consumption trends but overestimated demand during weekends.

Pruned Model Performance

Pruning led to minimal loss in accuracy:

MSE: 15.79

MAE: 3.90

The weights histogram indicated that pruning effectively removed less critical connections while retaining core features, as seen in the distributions of kernel, recurrent kernel, and bias weights.

Comparison and Visualizations

Visual comparisons between pruned and non-pruned models highlighted similar performance trends. Differences were mainly noticeable in outlier regions (weekend spikes), where the pruned model slightly underperformed.

Discussion

The results indicate that pruning significantly reduced model complexity without substantially degrading performance. This is crucial for real-world applications where computational resources are limited, such as edge devices or embedded systems in energy grids.

Key decisions in model design include:

Activation Function (ReLU): ReLU ensures faster computation and avoids saturation issues in deep networks. Alternate functions like tanh were avoided due to higher computational cost and potential for vanishing gradients.

Number of Units: Fifty units were chosen to balance complexity and predictive capacity. Higher unit counts showed diminishing returns in accuracy but increased training time and risk of overfitting.

Limitations

Weekend variations were not captured as effectively by the pruned model.

Future studies could explore hybrid architectures or external factors (e.g., weather) to improve robustness.

Conclusion

This study demonstrates the viability of pruning in LSTM models for electricity consumption forecasting. By achieving significant model compression with negligible accuracy loss, pruning paves the way for deploying efficient models in energy systems. Future work could include adaptive pruning strategies and integration with other time series features to enhance predictive accuracy.

The comparative results reinforce the trade-off between model complexity and computational cost, emphasizing the potential of LSTM pruning as a scalable solution for resource-constrained environments.
