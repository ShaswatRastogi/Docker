

# Docker
This Repo helps in running streamlit application using docker
=======
# Streamlit Dockerized Application

## 🚀 Overview

This guide explains how to containerize a **Streamlit** application using **Docker** and push it to a GitHub repository.

## 📂 Project Structure

```
Streamlit_Docker/
│── .streamlit/
│   └── config.toml
│── src/
│   └── app.py
│── Dockerfile
│── requirements.txt
│── README.md
```

## 🛠 Prerequisites

Before setting up, ensure you have:

- **Docker** installed and running 🐳
- **Python 3.9+** installed 🐍
- **Git** installed and configured
- \*\*A GitHub repository named \*\*``

---

## 🔧 Step 1: Create and Configure the Streamlit Application

### \*\*1️⃣ Create \*\*``

This file configures Streamlit settings:

```toml
[server]
headless = true
runOnSave = true
fileWatcherType = "poll"
```

### \*\*2️⃣ Create \*\*``

This is the main Streamlit application file:

```python
from collections import namedtuple
import altair as alt
import math
import pandas as pd
import streamlit as st

"""
# Welcome to Streamlit!

Edit `/src/app.py` to customize this app to your heart's desire ❤️

If you have any questions, checkout our [documentation](https://docs.streamlit.io) and [community forums](https://discuss.streamlit.io).
"""

with st.echo(code_location='below'):
    total_points = st.slider("Number of points in spiral", 1, 5000, 2000)
    num_turns = st.slider("Number of turns in spiral", 1, 100, 9)

    Point = namedtuple('Point', 'x y')
    data = []
    points_per_turn = total_points / num_turns

    for curr_point_num in range(total_points):
        curr_turn, i = divmod(curr_point_num, points_per_turn)
        angle = (curr_turn + 1) * 2 * math.pi * i / points_per_turn
        radius = curr_point_num / total_points
        x = radius * math.cos(angle)
        y = radius * math.sin(angle)
        data.append(Point(x, y))

    st.altair_chart(alt.Chart(pd.DataFrame(data), height=500, width=500)
        .mark_circle(color='#0068c9', opacity=0.5)
        .encode(x='x:Q', y='y:Q'))
```

### \*\*3️⃣ Create \*\*``

This file contains the dependencies:

```txt
streamlit
```

### \*\*4️⃣ Create \*\*``

Defines the containerized environment:

```dockerfile
FROM python:3.9
WORKDIR /app
COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8501
CMD ["streamlit", "run", "src/app.py", "--server.address=0.0.0.0", "--server.port=8501"]
```

---

## 🔨 Step 2: Build and Run the Docker Container

### **1️⃣ Navigate to the Project Folder**

```sh
cd "D:/Full Docker/Streamlit_Docker"
```

### **2️⃣ Build the Docker Image**

```sh
docker build -t streamlit-app .
```

### **3️⃣ Run the Container**

```sh
docker run -p 8501:8501 streamlit-app
```

### **4️⃣ Access the Application**

Open your browser and go to:

```
http://localhost:8501
```

---

## 📤 Step 3: Push the Project to GitHub

### **1️⃣ Initialize Git (If Not Already Initialized)**

```sh
git init
```

### **2️⃣ Add the Remote Repository (If Not Added)**

```sh
/
```

### **3️⃣ Add All Files to Git**

```sh
git add .
```

### **4️⃣ Commit the Changes**

```sh
git commit -m "Added Streamlit Docker experiment"
```

### **5️⃣ Push to GitHub**

```sh
git push origin main
```

👉 **(Use **``** instead of **``** if your repository uses **``** as the default branch.)**

---

## 🎯 Conclusion

✅ **Dockerized Streamlit app is running successfully.** ✅ **Project is pushed to GitHub.** ✅ **Ready for further development and deployment!** 🚀
