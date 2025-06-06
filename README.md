# Bivariate Data Analysis Project: Exploring Relationships Through Visualization

## Project Overview

This project delves into **Bivariate Data Analysis**, a fundamental step in understanding how two variables interact and influence each other within a dataset. By employing various statistical plotting techniques, I explored relationships between different pairs of features (numerical-numerical, numerical-categorical, categorical-categorical) to uncover patterns, trends, and insights.

The project utilizes popular Python libraries for data manipulation and visualization, including `pandas`, `numpy`, `seaborn`, and `matplotlib`, across several well-known datasets.

## Datasets Used

This project demonstrates bivariate analysis using the following datasets:

* **`tips`**: A dataset containing information about restaurant tips.
* **`flights`**: A dataset tracking monthly passenger numbers on commercial flights.
* **`titanic`**: The classic dataset containing passenger information from the Titanic voyage.
* **`iris`**: The famous dataset comprising measurements of iris flowers.

## Key Analysis and Visualization Techniques

The following sections detail the types of bivariate plots generated, their purpose, and the specific variables analyzed.

### 1. Numerical - Numerical Relationships

These plots are designed to visualize the relationship between two continuous numerical variables.

* **Scatterplot**
    * **Purpose:** To show the relationship between two numerical variables, where each point represents an observation. It helps identify correlations, clusters, and outliers.
    * **Example Code:**
        ```python
        sns.scatterplot(x=tips['total_bill'], y=tips['tip'], hue=tips['sex'], style=tips['smoker'], size=tips['size'])
        ```
    * **Analysis:** Explored how `total_bill` relates to `tip`, further differentiating by `sex`, `smoker` status, and `size` of the dining party.

* **Lineplot**
    * **Purpose:** Primarily used to visualize trends over time or sequences for two numerical variables.
    * **Example Code:**
        ```python
        # Data preparation for time-series aggregation
        new = flights.groupby('year').sum(numeric_only=True).reset_index()
        sns.lineplot(x=new['year'], y=new['passengers'])
        ```
    * **Analysis:** Showcased the trend of `passengers` over `year` from the `flights` dataset after aggregating passenger numbers annually.

### 2. Numerical - Categorical Relationships

These plots help in understanding the distribution of a numerical variable across different categories of a categorical variable.

* **Bar Plot**
    * **Purpose:** To display the central tendency (typically mean) of a numerical variable for different groups of a categorical variable. Confidence intervals are usually shown.
    * **Example Code (Age by Pclass):**
        ```python
        sns.barplot(x=titanic['Pclass'], y=titanic['Age'])
        ```
    * **Example Code (Fare by Pclass, differentiated by Sex):**
        ```python
        sns.barplot(x=titanic['Pclass'], y=titanic['Fare'], hue=titanic['Sex'])
        ```
    * **Analysis:** Investigated the average `Age` and `Fare` across different `Pclass` (passenger class) on the Titanic, also observing differences based on `Sex`.

* **Box Plot**
    * **Purpose:** To visualize the distribution (median, quartiles, and outliers) of a numerical variable for each category of a categorical variable.
    * **Example Code:**
        ```python
        sns.boxplot(x=titanic['Sex'], y=titanic['Age'], hue=titanic['Survived'])
        ```
    * **Analysis:** Compared the `Age` distribution between males and females, further segmented by their `Survived` status, revealing insights into age and gender survival patterns.

* **Distribution Plot (KDE overlay)**
    * **Purpose:** To compare the probability density distributions of a numerical variable across different categories. Using Kernel Density Estimate (KDE) provides a smooth representation of the data's density.
    * **Example Code (Age distribution by Survival status):**
        ```python
        sns.kdeplot(titanic[titanic['Survived'] == 0]['Age'], label='Not Survived')
        sns.kdeplot(titanic[titanic['Survived'] == 1]['Age'], label='Survived')
        plt.legend()
        ```
    * **Analysis:** Compared the `Age` distributions of passengers who `Survived` versus those who `Not Survived` on the Titanic, highlighting potential age-related survival differences.

### 3. Categorical - Categorical Relationships

These plots are used to explore the relationship and frequencies between two or more categorical variables.

* **Heatmap (from Cross-tabulation)**
    * **Purpose:** To visualize the magnitude of the relationship between two categorical variables, often using a cross-tabulation (frequency table). Higher values are represented by more intense colors.
    * **Example Code:**
        ```python
        sns.heatmap(pd.crosstab(titanic['Pclass'], titanic['Survived']))
        ```
    * **Analysis:** Showed the frequency of `Survived` status across different `Pclass` categories, providing a clear visual of passenger class impact on survival.

* **ClusterMap (from Cross-tabulation)**
    * **Purpose:** Similar to a heatmap but with added hierarchical clustering, which reorders rows and columns to bring similar categories closer together, revealing underlying patterns.
    * **Example Code:**
        ```python
        sns.clustermap(pd.crosstab(titanic['SibSp'], titanic['Survived']))
        ```
    * **Analysis:** Visualized the relationship between the number of `SibSp` (siblings/spouses aboard) and `Survived` status, with clustering to highlight groups with similar survival rates based on family size.

### 4. Multivariate (Multiple Variable) Relationship

* **Pairplot**
    * **Purpose:** To create a grid of scatterplots for numerical variables and histograms/KDEs for individual variables, optionally colored by a categorical variable. It's excellent for a quick overview of relationships within a dataset.
    * **Example Code:**
        ```python
        sns.pairplot(iris, hue='species')
        ```
    * **Analysis:** Generated a matrix of scatter plots for all numerical features in the `iris` dataset, with points colored by `species`, helping to identify feature combinations that best separate the different iris species.

## Technologies Used

* **Python**
* **Pandas:** For data loading, manipulation, and structured data analysis.
* **NumPy:** For numerical operations.
* **Seaborn:** For creating high-level, aesthetically pleasing statistical graphics.
* **Matplotlib:** For foundational plotting capabilities and fine-grained plot customization.


