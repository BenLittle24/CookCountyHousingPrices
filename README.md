# **Cook County Housing Prices**

## **Overview**
This project uses linear regression modeling to predict housing prices in Cook County, Illinois, based on multiple variables. It explores systemic inequities in housing assessments and how predictive modeling could improve fairness and accuracy, as well as a discussion about what that means. The project involves building and evaluating several models to minimize residual mean square error (RMSE) and analyzing the implications of statistical modeling in addressing disparities in property taxation.

---

## **Motivation**
This project was developed as a final project for my recent course in Data Science Algorithms with Probability and Statistics (CSPB 3022), and served as both a learning experience and an exploration of housing inequities. The project began with guided steps for modeling and gradually introduced more autonomy in feature selection and model improvement. Specifically, the project required:
- Building initial linear models with some instructor guidance.
- Exploring additional quantitative features to reduce RMSE.
- Designing a final model with full control over feature selection, enabling independent exploration and learning.

The project highlights how data science techniques can address real-world problems, such as regressive taxation, and contribute to equitable solutions.

---

## **Dataset**
The dataset was provided as part of the course and includes housing assessment data from Cook County, Illinois. Key features in the dataset include:
- **Property Value**: The primary target variable (`Sale Price`) for prediction.
- **Neighborhood Characteristics**: Features describing the location and community context of the property.
- **Property Characteristics**: Features describing the physical characters of a property, such as whether it had central air conditioning, the roof material, wall material, square footage, etc. 
- **Assessment Data**: Estimated value of a property as calculated by the Cook County property assessment office. 

The dataset was split into training/validation and test sets. The test set was intentionally left without the `Sale Price` target feature to simulate real-world prediction scenarios.

---

## **Methodology**
This project followed a structured workflow to build and refine linear regression models:
1. **Initial Modeling**: Guided modeling with a focus on building a baseline using provided features.
2. **Feature Exploration**: Experimentation with additional quantitative features to enhance prediction accuracy.
3. **Custom Model Development**: Full control over feature selection, transformations, and interactions to optimize RMSE and find impactful additions/relationships. For further detail, see [here](EC%20Writeup.md). 

### **Tools and Libraries**
The following tools and libraries were essential for the project:
- **Python**: Core programming language for analysis.
- **Pandas**: Data manipulation and preprocessing.
- **NumPy**: Numerical computations.
- **Matplotlib & Seaborn**: Data visualization.
- **scikit-learn**: Machine learning model development.
- **Plotly**: Interactive visualizations (minor part of the project, but helpful)
- **Jupyter Notebook**: Interactive environment for coding and analysis.

---

## **Results**
- **Model Performance**:
  - The third model achieved a training RMSE of ~242k and a validation RMSE of ~247k, serving as a baseline for further improvements.
  - The final model significantly improved upon these results, achieving a training RMSE of ~186k and a validation RMSE of ~194k. This represents a notable reduction in prediction error while adhering to assignment guidelines and logical feature selection, which I (embarrassingly) did deviate from at a point during my exploration. A more detailed explanation of this can be found in the [Extra Credit](EC%20Writeup.md) writeup. 
  - Residual plots for the final model show a tighter clustering around zero, indicating improved predictive accuracy compared to earlier models. Some slight underestimation of lower-priced houses remains, but overall residual patterns are much less pronounced.

- **Insights**:
  - Feature engineering and selection were critical in improving model performance. Notable contributions to the final model included:
    - **Log Estimate (Land)** and **Log Estimate (Building)**: Strong predictors that replaced problematic Sale Price-based features such as **Log Price per Square Foot** to comply with test set restrictions.
    - **Central Air** and **Roof Material**: Demonstrated strong correlations with housing prices and meaningful interactions with other features.
    - **Property Class**: Provided a logical and intuitive relationship to housing prices, improving model performance.
  - The inclusion of interaction terms, such as **Log Estimate (Building) x Central Air**, further refined the model by capturing nuanced relationships between features.

- **Challenges and Iterations**:
  - Experimentation with features like **Log Price per Square Foot** initially yielded low RMSE values but introduced issues of overfitting due to collinearity. This feature was eventually removed after I remembered that `Sale Price` was not included in the test dataset and the logic behind this exclusion.
  - Attempts to incorporate additional qualitative features like **Town and Neighborhood** were delayed by encoding challenges. While these features showed promise in early analysis, I achieved RMSE values below the 200k target before revisiting them. Unfortunately, this led to their exclusion from the final model, though these features might still provide value. 
  - For a more in-depth record of the iterations, check [this](EC%20Writeup.md) out. 

---

## **How to Run**
This project originated as a JupyterHub Notebook in my university coding environment and included an autograder, but can be reproduced outside of this environment. At the time of writing, I don’t believe there is a way to include the autograder (Otter Grader) functionality because the test cases were hidden, though this exclusion shouldn’t impact overall functionality. 

If you’d like to replicate or further explore this project, there are a number of ways to do so independent of my university’s coding environment. For example, you can set up a local environment on your own machine and use a platform like VS Code or Jupyter Notebook. These steps should be a good starting point: 

1. **Clone the repository**
2. **Navigate to the project directory**
3. **Set Up Your Environment**:
   - **Option 1: VS Code** (my recommendation)
     - If necessary, install the Jupyter extension for VS Code. 
     - Open the `.ipynb` file directly in VS Code.
     - Run cells sequentially (ignoring autograder cells), this should ensure that required libraries are imported. 
   - **Option 2: Jupyter Notebook**  
     - For this approach, set up a virtual environment and install dependencies. Example:
       ```bash
       python -m venv env
       source env/bin/activate  # Use .\env\Scripts\activate if you're on Windows
       pip install pandas numpy matplotlib seaborn scikit-learn notebook
       ```
     - Run the notebook:
       ```bash
       jupyter notebook
       ```
     - Open `.ipynb` file and run the cells sequentially (ignoring autograder cells).

---

## **Acknowledgments**
This project was developed as an academic assignment. Special thanks to the course instructors for their guidance and everyone involved in creating this dataset. 
