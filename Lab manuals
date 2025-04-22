<!DOCTYPE html>
<html>
<head>
  <title>ML Lab Website</title>
  <style>
    body {
      font-family: sans-serif;
      background: #f9f9f9;
      margin: 0;
    }
    nav {
      background: #333;
      color: white;
      display: flex;
      padding: 10px;
    }
    nav a {
      color: white;
      margin-right: 20px;
      text-decoration: none;
      font-weight: bold;
    }
    .content {
      display: none;
      padding: 20px;
    }
    .active {
      display: block;
    }
    pre {
      background: #fff;
      padding: 15px;
      border-radius: 5px;
      overflow-x: auto;
      font-family: monospace;
    }
    iframe {
      width: 100%;
      height: 600px;
      border: none;
    }
  </style>
</head>
<body>
  <nav>
    <a href="#" onclick="showTab('exp3')">EXP-3</a>
    <a href="#" onclick="showTab('mlLab')">ML-LAB</a>
  </nav>

  <div id="exp3" class="content active">
    <h2>Experiment 3 - Decision Tree</h2>
    <pre>
import math
import pandas as pd
def calculate_entropy(data):
    value_counts = data.value_counts()
    total_records = len(data)
    entropy = 0
    for count in value_counts:
        prob = count / total_records
        entropy -= prob * math.log2(prob)
    return entropy

def calculate_information_gain(data, attribute, target):
    total_entropy = calculate_entropy(data[target])
    unique_values = data[attribute].unique()
    weighted_entropy = 0
    for value in unique_values:
        subset = data[data[attribute] == value]
        weighted_entropy += (len(subset) / len(data)) * calculate_entropy(subset[target])
    information_gain = total_entropy - weighted_entropy
    return information_gain

def id3(data, target, attributes):
    if len(data[target].unique()) == 1:
        return data[target].iloc[0]
    if not attributes:
        return data[target].mode()[0]
    info_gains = {attr: calculate_information_gain(data, attr, target) for attr in attributes}
    best_attribute = max(info_gains, key=info_gains.get)
    tree = {best_attribute: {}}
    for value in data[best_attribute].unique():
        subset = data[data[best_attribute] == value]
        remaining_attributes = [attr for attr in attributes if attr != best_attribute]
        subtree = id3(subset, target, remaining_attributes)
        tree[best_attribute][value] = subtree
    return tree

def classify(tree, sample):
    if not isinstance(tree, dict):
        return tree
    attribute = next(iter(tree))
    attribute_value = sample[attribute]
    subtree = tree[attribute].get(attribute_value)
    return classify(subtree, sample)

# Sample data and call
data = pd.DataFrame({
    'Outlook': ['Sunny', 'Sunny', 'Overcast', 'Rainy', 'Rainy', 'Rainy', 'Overcast', 'Sunny', 'Sunny', 
                'Rainy', 'Sunny', 'Overcast', 'Overcast', 'Rainy'],
    'Temperature': ['Hot', 'Hot', 'Hot', 'Mild', 'Cool', 'Cool', 'Cool', 'Mild', 'Cool', 'Mild', 'Mild', 'Mild', 
                    'Hot', 'Mild'],
    'Humidity': ['High', 'High', 'High', 'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'Normal', 
                 'Normal', 'High', 'Normal', 'High'],
    'Wind': ['Weak', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Weak', 'Weak', 
             'Strong', 'Strong', 'Weak', 'Strong'],
    'PlayTennis': ['No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes', 'No', 'Yes', 'Yes', 'Yes', 'Yes', 'Yes', 'No']
})
target = 'PlayTennis'
attributes = ['Outlook', 'Temperature', 'Humidity', 'Wind']
tree = id3(data, target, attributes)
print("Decision Tree:")
print(tree)
sample = {'Outlook': 'Sunny', 'Temperature': 'Hot', 'Humidity': 'High', 'Wind': 'Weak'}
result = classify(tree, sample)
print(f"\nClassifying new sample {sample}: {result}")
    </pre>
  </div>

  <div id="mlLab" class="content">
    <h2>ML-LAB PDF</h2>
    <iframe src="https://drive.google.com/file/d/1rxTNSsfOiMvcMDNFcS1K_IQla86DyiJD/preview" allow="autoplay"></iframe>
  </div>

  <script>
    function showTab(tabId) {
      document.querySelectorAll('.content').forEach(c => c.classList.remove('active'));
      document.getElementById(tabId).classList.add('active');
    }
  </script>
</body>
</html>
