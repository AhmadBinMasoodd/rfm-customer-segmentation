# 🧠 RFM Customer Segmentation – E-commerce Data Analysis

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-1.3+-green.svg)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.4+-red.svg)
![Seaborn](https://img.shields.io/badge/Seaborn-0.11+-orange.svg)

This project applies **RFM (Recency, Frequency, Monetary) analysis** to segment customers based on their purchasing behavior using real-world data from a Brazilian e-commerce platform (Olist).

## 📌 Objective

The goal is to identify different customer segments like **Champions**, **Loyal Customers**, **Big Spenders**, **Recent Customers**, **Frequent Buyers**, and others to enable better targeting in marketing strategies and customer retention efforts.

---

## 📂 Dataset Used

**Brazilian E-Commerce Public Dataset by Olist** (via Kaggle)

The dataset contains comprehensive information about:
- 📦 **Orders**: Order details, timestamps, and status
- 👥 **Customers**: Customer demographics and location
- 💳 **Payments**: Payment methods and values
- ⭐ **Reviews**: Customer feedback and ratings
- 🛍️ **Products**: Product categories and details
- 🏪 **Sellers**: Seller information and location
- 📍 **Geolocation**: Geographic coordinates

### Dataset Files:
```
├── olist_customers_dataset.csv
├── olist_geolocation_dataset.csv
├── olist_orders_dataset.csv
├── olist_order_items_dataset.csv
├── olist_order_payments_dataset.csv
├── olist_order_reviews_dataset.csv
├── olist_products_dataset.csv
├── olist_sellers_dataset.csv
└── product_category_name_translation.csv
```

---

## 📊 Methodology

### 1. **Data Cleaning & Preprocessing**
- Load and explore multiple datasets
- Handle missing values and data types
- Merge relevant tables to create a unified dataset
- Convert timestamp columns to datetime format

### 2. **RFM Metric Calculation**

#### 🕒 **Recency (R)**
- **Definition**: Days since the customer's last purchase
- **Calculation**: `Reference Date - Last Purchase Date`
- **Interpretation**: Lower recency = More recent customer

#### 🔄 **Frequency (F)**
- **Definition**: Total number of purchases made by the customer
- **Calculation**: Count of unique orders per customer
- **Interpretation**: Higher frequency = More loyal customer

#### 💰 **Monetary (M)**
- **Definition**: Total amount spent by the customer
- **Calculation**: Sum of all purchase amounts per customer
- **Interpretation**: Higher monetary = More valuable customer

### 3. **RFM Scoring System**
- **Scoring Range**: 1-5 scale for each metric
- **Method**: Quantile-based segmentation using `pd.qcut()`
- **Recency Scoring**: 5 = Most recent, 1 = Least recent
- **Frequency Scoring**: 5 = Most frequent, 1 = Least frequent
- **Monetary Scoring**: 5 = Highest spender, 1 = Lowest spender

### 4. **Customer Segmentation Logic**

```python
def segment_customer(row):
    if row['rfm_score'] == '555':
        return 'Champions'                    # Best customers (Recent, Frequent, High-value)
    elif row['r_score'] == 5 and row['f_score'] >= 4:
        return 'Loyal Customers'             # Recent and frequent buyers
    elif row['r_score'] >= 4:
        return 'Recent Customers'            # Recently active customers
    elif row['f_score'] >= 4:
        return 'Frequent Buyers'             # High-frequency purchasers
    elif row['m_score'] >= 4:
        return 'Big Spenders'                # High-value customers
    else:
        return 'Others'                      # Remaining customers
```

---

## 🛠️ Tools & Libraries

### **Core Libraries**
- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **matplotlib**: Data visualization
- **seaborn**: Statistical data visualization

### **Python Environment**
- **Python 3.8+**
- **Jupyter Notebook**: Interactive development environment

### **Installation**
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

---

## 📈 Results & Key Insights

### **Customer Segment Distribution**

| Segment          | Count  | Percentage |
|------------------|--------|------------|
| Recent Customers | 31,648 | 32.4%      |
| Frequent Buyers  | 23,744 | 24.3%      |
| Others           | 21,514 | 22.0%      |
| Big Spenders     | 13,850 | 14.2%      |
| Loyal Customers  | 7,122  | 7.3%       |
| Champions        | 788    | 0.8%       |

### **Key Findings**

#### 🏆 **Champions (0.8%)**
- **Profile**: Best customers with high recency, frequency, and monetary scores
- **Strategy**: VIP treatment, exclusive offers, early access to new products

#### 💎 **Loyal Customers (7.3%)**
- **Profile**: Recent and frequent buyers with good spending habits
- **Strategy**: Loyalty programs, personalized recommendations

#### 🕒 **Recent Customers (32.4%)**
- **Profile**: Recently made purchases but may be new or infrequent buyers
- **Strategy**: Welcome campaigns, onboarding sequences, encourage repeat purchases

#### 🔄 **Frequent Buyers (24.3%)**
- **Profile**: Purchase regularly but may not be high spenders
- **Strategy**: Volume discounts, bundle offers, upselling opportunities

#### 💸 **Big Spenders (14.2%)**
- **Profile**: High-value customers who may not purchase frequently
- **Strategy**: Premium products, exclusive collections, retention campaigns

#### 📊 **Others (22.0%)**
- **Profile**: Customers with lower engagement across all metrics
- **Strategy**: Re-engagement campaigns, win-back offers, market research

---

## 📁 Project Structure

```
RFM-Customer-Segmentation/
│
├── 📊 Data Files/
│   ├── olist_customers_dataset.csv
│   ├── olist_geolocation_dataset.csv
│   ├── olist_orders_dataset.csv
│   ├── olist_order_items_dataset.csv
│   ├── olist_order_payments_dataset.csv
│   ├── olist_order_reviews_dataset.csv
│   ├── olist_products_dataset.csv
│   ├── olist_sellers_dataset.csv
│   └── product_category_name_translation.csv
│
├── 📓 Analysis/
│   └── solution.ipynb                    # Main analysis notebook
│
├── 📈 Output/
│   └── rfm_segmented_customers.csv       # Final segmented customer data
│
└── 📋 Documentation/
    └── README.md                         # Project documentation
```

---

## 🚀 Getting Started

### **Prerequisites**
1. Python 3.8 or higher
2. Jupyter Notebook or JupyterLab
3. Required Python packages (see requirements below)

### **Installation Steps**

1. **Clone or download the repository**
```bash
git clone <repository-url>
cd RFM-Customer-Segmentation
```

2. **Install required packages**
```bash
pip install -r requirements.txt
```

3. **Launch Jupyter Notebook**
```bash
jupyter notebook
```

4. **Open and run `solution.ipynb`**

### **Requirements.txt**
```txt
pandas>=1.3.0
numpy>=1.21.0
matplotlib>=3.4.0
seaborn>=0.11.0
jupyter>=1.0.0
```

---

## 🔍 Analysis Workflow

### **Step 1: Data Loading & Exploration**
- Load all CSV files
- Examine data structure and quality
- Identify key relationships between tables

### **Step 2: Data Preprocessing**
- Merge customer, order, and order items data
- Handle missing values and data type conversions
- Create a unified dataset for analysis

### **Step 3: RFM Calculation**
- Calculate Recency: Days since last purchase
- Calculate Frequency: Total number of orders
- Calculate Monetary: Total purchase amount

### **Step 4: RFM Scoring**
- Apply quantile-based scoring (1-5 scale)
- Create composite RFM score
- Generate meaningful customer segments

### **Step 5: Visualization & Analysis**
- Customer segment distribution charts
- Revenue analysis by segment
- Identify top customers in each segment

### **Step 6: Export Results**
- Save segmented customer data to CSV
- Generate actionable insights and recommendations

---

## 📊 Visualizations

The project includes several key visualizations:

1. **📈 Customer Segment Distribution**: Bar chart showing the count of customers in each segment
2. **💰 Revenue by Segment**: Analysis of total revenue contribution from each customer segment
3. **🏆 Top Champions**: Detailed view of the highest-value customers

---

## 💡 Business Applications

### **Marketing Strategies**
- **Targeted Campaigns**: Customize marketing messages for each segment
- **Budget Allocation**: Focus resources on high-value segments
- **Customer Retention**: Develop specific retention strategies for each group

### **Product Development**
- **Feature Prioritization**: Develop features that appeal to Champions and Loyal Customers
- **Pricing Strategy**: Create pricing tiers that match customer value segments

### **Customer Service**
- **Support Prioritization**: Provide premium support to Champions and Loyal Customers
- **Communication Frequency**: Adjust communication cadence based on customer segment

---

## 🔮 Future Enhancements

1. **🤖 Machine Learning Integration**
   - Implement clustering algorithms (K-Means, DBSCAN)
   - Predictive modeling for customer lifetime value

2. **⏰ Time-Series Analysis**
   - Seasonal purchasing patterns
   - Customer journey mapping

3. **📊 Advanced Segmentation**
   - Geographic segmentation
   - Product category preferences
   - Multi-dimensional customer personas

4. **🔄 Real-Time Updates**
   - Automated daily/weekly RFM updates
   - Dynamic customer segment migration tracking

5. **📱 Dashboard Development**
   - Interactive web dashboard using Streamlit or Dash
   - Real-time monitoring and alerts

---

## 📚 References

- [RFM Analysis Guide](https://en.wikipedia.org/wiki/RFM_(customer_value))
- [Brazilian E-Commerce Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- [Customer Segmentation Best Practices](https://blog.hubspot.com/service/what-does-it-mean-to-segment-customers)

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

---



## 👨‍💻 Author

**Ahmad Bin Masood**
- GitHub: [@AhmadBinMasoodd](https://github.com/AhmadBinMasoodd)
- LinkedIn: [Ahmad Bin Masood](https://www.linkedin.com/in/ahmad-bin-masood-3774aa278/)
- Email: ahmadbinmasood@example.com

---

## 🙏 Acknowledgments

- **Olist** for providing the comprehensive e-commerce dataset
- **Kaggle** for hosting the dataset and community
- **Python Community** for the amazing data science libraries

---

*⭐ If you found this project helpful, please give it a star on GitHub! ⭐*
