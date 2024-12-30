To develop the extra credit model, I first searched for features with strong correlations to Log Sale Price, particularly qualitative features that were excluded from Model 3\. There were dozens of iterations and experiments to identify impactful variables and interactions. Here is a summary of the steps taken:

1. Initial Exploration and Model:   
   1. I started by evaluating correlations between Log Sale Price and various qualitative features, selecting primarily based on how much I expected they would factor into Sale Price. Property Class was my first standout feature, it had a good correlation and the relationship to Sale Price felt intuitive.   
   2. The first model included Log Building Square Feet, Log Sale Price, and Property Class. This initial model resulted in a higher RMSE than Model 3\.   
2. Adding Model 3 Features:   
   1. To try to match or exceed Model 3’s performance, I added Roof Material and Land Square Feet. This did improve the RMSE, but it was only marginally better than Model 3\.   
3. Adding Central Air:   
   1. After recognizing the strong correlation between Central Air and Log Sale Price, I added it to the model as well. This was an improvement as well, but not significantly.  
4. Testing Age and Utilizing Feature Coefficients:  
   1. I briefly included Age due to its moderate correlation, but it resulted in virtually zero improvement.   
   2. At this point I also began checking Feature or Linear Regression Coefficients to factor in the strength and direction of the relationship between each feature and Log Sale Price. With this data, I saw how little Age and Land Square Feet were contributing, so these were removed.   
5. Experimenting with Feature Interactions:   
   1. So far, I had not improved on Model 3’s RMSE in any significant way, so I tested some interaction terms:   
      1. Central Air x Roof Material and Central Air x Log Building Square Feet showed meaningful improvement, so I kept these terms.   
      2. I also tested Property Class x Log Building Square Feet, but it had little effect on RMSE, so I removed it.   
6. Standardization of Features:   
   1. I briefly standardized Log Building Square Feet, but this failed to improve RMSE, so I reverted back to the original scale.   
7. Breakthrough with Price per Square Foot:   
   1. Introducing Price per Square Foot and its log transformation caused a significant drop in RMSE. However, the training RMSE value was effectively 0, which seemed too good to be true and indicative of a problematic model.   
   2. After a closer look, I realized that Log Price per Sqft was highly collinear with Log Building Square Feet and other variables, causing the model to overfit.   
8. Refining Log Price per Sqft:   
   1. To address the collinearity issue without losing the benefits of Log Price per Sqft, I tried using Log Price per Sqft in interactions instead of on its own. I created:   
      1. Log Price per Sqft x Property Class  
      2. Log Price per Sqft x Central Air  
      3. (Log Price per Sqft)^2  
   2. These versions produced more realistic RMSE values, all under the goal of 200k. Log Price per Sqft x Property Class was the best iteration with the lowest RMSE:   
      1. Training RMSE: 75,368  
      2. Validation RMSE: 95,407  
9. Downfall of Log Price per Sqft:   
   1. Regrettably, in my excitement about the low RMSE values, I overlooked the guidelines, my own code comments, and consequently forgot that Sale Price was not included in the test data. So my beloved Log Price per Sqft feature was doomed to shine only in my heart and the training data. With quiet resignation, I pressed onward.  
10. Adding Estimate Features:   
    1. After the painful realization that Log Price per Sqft was unusable for the test set, I pivoted to features that would be available in both the training and test data. Estimate (Land) and Estimate (Building) both had strong correlations with Log Sale Price, and were similar enough in nature to the Sale Price based features that I thought they might have a similar effect on RMSE. Both were log transformed to align with the model’s existing features. Interactions include:   
       1. Log Estimate (Land) x Property Class  
       2. Log Estimate (Building) x Central Air  
    2. The result of these additions was a significant reduction in RMSE, bringing the model from roughly 230k to below 200k.   
11. Challenges with Incorporating Town and Neighborhood:   
    1. I attempted to include Town and Neighborhood, which had promising correlations with Log Sale Price. Unfortunately, one-hot encoding errors prevented this. I tried multiple fixes, including a global encoder at one point, but I wasn’t able to solve the issues. I intended on coming back to this problem after exploring alternative features, but the alternatives ended up being successful. 

The final model uses a combination of Log Building Sqft, Central Air, Roof Material, Property Class, Log Estimate (Land), and Log Estimate (Building) features to achieve a Training RMSE of about 186,441 and Validation RMSE of about 194,739. While this is substantially higher than the RMSE from the model including Log Price per Sqft, these results better adhere to the logic and guidelines of the assignment, and they are still a marked improvement over Model 3\. 

The residual plots show a notable improvement compared to earlier versions as well. Residuals are now more tightly clustered around zero, indicating better overall model performance. There is a slight trend where the lower priced houses have positive residuals, suggesting some underestimation, but all patterns are much less pronounced compared to earlier models. While there is room for further refinement, the improvements reflect the effectiveness of the new features.  