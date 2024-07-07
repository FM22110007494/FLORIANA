#1. Data Visualization:
#Using Python libraries such as Matplotlib and Seaborn to create visualizations.

#Sales Trends Over Time:

import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

# Load the dataset
df = pd.read_csv('customer_purchases.csv')

# Convert date column to datetime
df['purchase_date'] = pd.to_datetime(df['purchase_date'])

# Plot sales trends
plt.figure(figsize=(10, 6))
sns.lineplot(x='purchase_date', y='amount_spent', data=df)
plt.title('Sales Trends Over Time')
plt.xlabel('Date')
plt.ylabel('Amount Spent')
plt.show()

Customer Segmentation:


plt.figure(figsize=(10, 6))
sns.boxplot(x='customer_segment', y='amount_spent', data=df)
plt.title('Amount Spent by Customer Segment')
plt.xlabel('Customer Segment')
plt.ylabel('Amount Spent')
plt.show()
#2. Data Dashboard:
#Using Plotly and Dash to create an interactive dashboard.


import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
import plotly.express as px

# Initialize the Dash app
app = dash.Dash(__name__)

# Define the layout
app.layout = html.Div([
    html.H1("Customer Purchase Dashboard"),
    dcc.DatePickerRange(
        id='date-range',
        start_date=df['purchase_date'].min(),
        end_date=df['purchase_date'].max()
    ),
    dcc.Graph(id='sales-trends'),
    dcc.Graph(id='customer-segmentation')
])

# Define callback to update graphs
@app.callback(
    [Output('sales-trends', 'figure'), Output('customer-segmentation', 'figure')],
    [Input('date-range', 'start_date'), Input('date-range', 'end_date')]
)
def update_graphs(start_date, end_date):
    filtered_df = df[(df['purchase_date'] >= start_date) & (df['purchase_date'] <= end_date)]
    sales_trends_fig = px.line(filtered_df, x='purchase_date', y='amount_spent', title='Sales Trends Over Time')
    customer_segmentation_fig = px.box(filtered_df, x='customer_segment', y='amount_spent', title='Amount Spent by Customer Segment')
    return sales_trends_fig, customer_segmentation_fig

# Run the app
if __name__ == '__main__':
    app.run_server(debug=True)
#3. Data-Rich Report:
#Creating a detailed report in a Jupyter Notebook.


import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv('customer_purchases.csv')

# Data preprocessing
df['purchase_date'] = pd.to_datetime(df['purchase_date'])

# Sales trends visualization
plt.figure(figsize=(10, 6))
sns.lineplot(x='purchase_date', y='amount_spent', data=df)
plt.title('Sales Trends Over Time')
plt.xlabel('Date')
plt.ylabel('Amount Spent')
plt.show()

# Customer segmentation visualization
plt.figure(figsize=(10, 6))
sns.boxplot(x='customer_segment', y='amount_spent', data=df)
plt.title('Amount Spent by Customer Segment')
plt.xlabel('Customer Segment')
plt.ylabel('Amount Spent')
plt.show()

# Summary statistics
summary_stats = df.describe()
print(summary_stats)
#4. Web-Accessible Python Notebook:
#Creating and sharing a Jupyter Notebook as an HTML file.


import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv('customer_purchases.csv')

# Data preprocessing
df['purchase_date'] = pd.to_datetime(df['purchase_date'])

# Sales trends visualization
plt.figure(figsize=(10, 6))
sns.lineplot(x='purchase_date', y='amount_spent', data=df)
plt.title('Sales Trends Over Time')
plt.xlabel('Date')
plt.ylabel('Amount Spent')
plt.show()

# Customer segmentation visualization
plt.figure(figsize=(10, 6))
sns.boxplot(x='customer_segment', y='amount_spent', data=df)
plt.title('Amount Spent by Customer Segment')
plt.xlabel('Customer Segment')
plt.ylabel('Amount Spent')
plt.show()
