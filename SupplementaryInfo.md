# Detailed information about regression task

## Difference between usual regression task
In usual regression tasks, we have input features X and output label y as one continuous scalar. You can freely choose the regression models, like LASSO, Elastic-net, Gaussian Process, XGBosst, and so on.
But, in the QS challenge, we cannot use the above regression models directly because our regression model is predetermined as equivalent circuit models (ECMs). We have 9 types of ECMs with a different number of parameters. By adding some values to the circuit parameters, we can simulate the impedance spectrum at given frequencies. Evaluating the errors between the observed and simulated data in both real and imaginary parts gives the metric of how good the parameters are.
Thus, we should do regression on impedance via ECMs, not for labels on the provided circuit parameters. The labels in the dataset are just a rough guide, which is not absolutely true. You’ll find that you can easily get better parameters than the provided labels.

## Metric of good circuit parameters
We should be careful about the definition of “good parameters”. The minimum error means the best?
No. Occam’s razor works here: less number of parameters should be better. But some observed impedances are too complicated to simulate with small parameters. We should be adaptive to the complexity from impedance data itself.
Another difficulty is the experimental noise. ECS experiments contain noises, which could depend on frequencies and amplitude (and temperature as hidden information, we cannot get it though). Thus, the minimum error could lead to overfitting.
One way is the cross-validation we adapt. This metric is robust against noise but not too good for Occam’s razor perspective. Thus there is room for improvement.