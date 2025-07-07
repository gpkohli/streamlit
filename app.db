
import streamlit as st
import sqlite3
import pandas as pd

def get_connection():
    return sqlite3.connect("app_data.db")

def show_users():
    st.header("User Management")
    conn = get_connection()
    cursor = conn.cursor()

    # Display users
    df = pd.read_sql_query("SELECT * FROM users", conn)
    st.dataframe(df)

    # Add new user
    st.subheader("Add New User")
    name = st.text_input("Name")
    email = st.text_input("Email")
    if st.button("Add User"):
        try:
            cursor.execute("INSERT INTO users (name, email) VALUES (?, ?)", (name, email))
            conn.commit()
            st.success("User added successfully.")
        except Exception as e:
            st.error(f"Error: {e}")

    # Update user
    st.subheader("Update User")
    user_id = st.number_input("User ID", min_value=1)
    new_name = st.text_input("New Name")
    new_email = st.text_input("New Email")
    if st.button("Update User"):
        try:
            cursor.execute("UPDATE users SET name=?, email=? WHERE id=?", (new_name, new_email, user_id))
            conn.commit()
            st.success("User updated successfully.")
        except Exception as e:
            st.error(f"Error: {e}")

    # Delete user
    st.subheader("Delete User")
    delete_id = st.number_input("User ID to Delete", min_value=1)
    if st.button("Delete User"):
        try:
            cursor.execute("DELETE FROM users WHERE id=?", (delete_id,))
            conn.commit()
            st.success("User deleted successfully.")
        except Exception as e:
            st.error(f"Error: {e}")

    conn.close()

def show_products():
    st.header("Product Management")
    conn = get_connection()
    cursor = conn.cursor()

    # Display products
    df = pd.read_sql_query("SELECT * FROM products", conn)
    st.dataframe(df)

    # Add new product
    st.subheader("Add New Product")
    name = st.text_input("Product Name")
    price = st.number_input("Price", min_value=0.0)
    if st.button("Add Product"):
        try:
            cursor.execute("INSERT INTO products (name, price) VALUES (?, ?)", (name, price))
            conn.commit()
            st.success("Product added successfully.")
        except Exception as e:
            st.error(f"Error: {e}")

    # Update product
    st.subheader("Update Product")
    product_id = st.number_input("Product ID", min_value=1)
    new_name = st.text_input("New Product Name")
    new_price = st.number_input("New Price", min_value=0.0)
    if st.button("Update Product"):
        try:
            cursor.execute("UPDATE products SET name=?, price=? WHERE id=?", (new_name, new_price, product_id))
            conn.commit()
            st.success("Product updated successfully.")
        except Exception as e:
            st.error(f"Error: {e}")

    # Delete product
    st.subheader("Delete Product")
    delete_id = st.number_input("Product ID to Delete", min_value=1)
    if st.button("Delete Product"):
        try:
            cursor.execute("DELETE FROM products WHERE id=?", (delete_id,))
            conn.commit()
            st.success("Product deleted successfully.")
        except Exception as e:
            st.error(f"Error: {e}")

    conn.close()

# Sidebar navigation
st.sidebar.title("Navigation")
page = st.sidebar.radio("Go to", ["Users", "Products"])

if page == "Users":
    show_users()
elif page == "Products":
    show_products()
