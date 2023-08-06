---
title: "Automating Restaurant Orders with Bash Scripting 🍕"
datePublished: Sun Aug 06 2023 15:59:40 GMT+0000 (Coordinated Universal Time)
cuid: clkzmq58g000e08lbh9pi43ot
slug: automating-restaurant-orders-with-bash-scripting
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691337471487/5227ef69-ac85-4017-b6fd-92d05871334f.gif
tags: linux, developer, devops, shell, 90daysofdevops

---

# **📍 Introduction:**

In this blog post, we will explore how to create a Bash-based restaurant order system using a shell script. The script, `restaurant_order.sh`, allows customers to view the menu, place their orders, and calculate the total bill. We will walk through the steps to execute the shell script and explain the problems it solves to provide a seamless dining experience.

### **🔍 Problem:**

Imagine a bustling restaurant with a manual order-taking process, where customers have to place orders through paper forms, and the staff manually calculates the total bill. This process is not only time-consuming but also prone to human errors. To address these challenges, we will automate the order system with a Bash script.

### **🔍 Solution:**

The Bash script, `restaurant_order.sh`, streamlines the restaurant's ordering process and eliminates manual errors. It provides the following functionalities:

📋 **Display the Menu:** The script reads the menu from the `menu.txt` file and displays it to the customers, showing each item along with its price.

🔢 **Handle Invalid User Input:** The script ensures that customers enter valid inputs for their orders, such as selecting a menu item that exists and entering a positive quantity.

💰 **Calculate Total Bill:** The script calculates the total bill based on the customer's order, ensuring accurate and error-free calculations.

### **🔍 Final Executable full script - restaurant\_order.sh**

* Create a new file named `restaurant_order.sh` and open it in a text editor.
    

```plaintext
#!/bin/bash

# Function to display the menu
display_menu() {
  echo "Welcome to The Hungry Bash!"
  echo "Menu:"
  echo "-------------------"

  while IFS=',' read -r item price; do
    echo "$item - ₹$price"
  done < menu.txt

  echo "-------------------"
}

# Function to prompt for valid input
get_valid_input() {
  local prompt="$1"
  local input

  while true; do
    read -p "$prompt" input

    # Check if input is a positive integer
    if [[ $input =~ ^[0-9]+$ ]]; then
      echo "$input"
      return
    else
      echo "Invalid input. Please enter a positive number."
    fi
  done
}

# Function to calculate the total bill
calculate_total_bill() {
  local order_file="$1"
  local total=0

  while IFS=',' read -r item quantity; do
    # Get the price of the item from the menu.txt file (case-insensitive search)
    local price=$(grep -i "^$item," menu.txt | cut -d',' -f2)

    # Check if the item exists in the menu
    if [[ -n "$price" ]]; then
      # Calculate the total price for this item and quantity
      local item_total=$((price * quantity))
      total=$((total + item_total))
    else
      echo "Invalid item: $item"
      exit 1
    fi
  done < "$order_file"

  echo "$total"
}


# Main script
display_menu

# Prompt user for order and quantity
order_file="order.txt"

while true; do
  read -p "Enter item name (or 'done' to finish): " item
  if [[ "$item" == "done" ]]; then
    break
  fi

  read -p "Enter quantity: " quantity
  while ! [[ "$quantity" =~ ^[0-9]+$ ]]; do
    echo "Invalid quantity. Please enter a positive number."
    read -p "Enter quantity: " quantity
  done

  echo "$item,$quantity" >> "$order_file"
done

# Calculate and display the total bill
total_bill=$(calculate_total_bill "$order_file")
echo "Your total bill: ₹$total_bill"
```

### **🔍 Step-by-Step Guide:**

**Step 1: Add Display Menu Function**

* Implement a function called `display_menu` to read and display the menu from the `menu.txt` file.
    

```plaintext
#!/bin/bash

# Function to display the menu
display_menu() {
  echo "Welcome to The Hungry Bash!"
  echo "Menu:"
  echo "-------------------"

  while IFS=',' read -r item price; do
    echo "$item - ₹$price"
  done < menu.txt

  echo "-------------------"
}
```

**Step 2: Add Invalid User Input Handling Function**

* Implement a function called `get_valid_input` to prompt users for valid inputs and handle errors.
    

```plaintext
# Function to prompt for valid input
get_valid_input() {
  local prompt="$1"
  local input

  while true; do
    read -p "$prompt" input

    # Check if input is a positive integer
    if [[ $input =~ ^[0-9]+$ ]]; then
      echo "$input"
      return
    else
      echo "Invalid input. Please enter a positive number."
    fi
  done
}
```

**Step 3: Add Total Bill Calculation Function**

* Implement a function called `calculate_total_bill` to calculate the total bill based on the customer's order.
    

```plaintext
# Function to calculate the total bill
calculate_total_bill() {
  local order_file="$1"
  local total=0

  while IFS=',' read -r item quantity; do
    # Get the price of the item from the menu.txt file (case-insensitive search)
    local price=$(grep -i "^$item," menu.txt | cut -d',' -f2)

    # Check if the item exists in the menu
    if [[ -n "$price" ]]; then
      # Calculate the total price for this item and quantity
      local item_total=$((price * quantity))
      total=$((total + item_total))
    else
      echo "Invalid item: $item"
      exit 1
    fi
  done < "$order_file"

  echo "$total"
}
```

**Step 4: Integrate Functions into the Main Script**

* In the main part of the script, call the `display_menu` function to show the menu to the customers.
    
* Prompt the user for their order and quantity and save it to a temporary order file.
    
* Call the `calculate_total_bill` function with the temporary order file to get the total bill.
    
* Display the total bill to the customer.
    

```plaintext
# Main script
display_menu

# Prompt user for order and quantity
order_file="order.txt"

while true; do
  read -p "Enter item name (or 'done' to finish): " item
  if [[ "$item" == "done" ]]; then
    break
  fi

  read -p "Enter quantity: " quantity
  while ! [[ "$quantity" =~ ^[0-9]+$ ]]; do
    echo "Invalid quantity. Please enter a positive number."
    read -p "Enter quantity: " quantity
  done

  echo "$item,$quantity" >> "$order_file"
done

# Calculate and display the total bill
total_bill=$(calculate_total_bill "$order_file")
echo "Your total bill: ₹$total_bill"
```

### **🔍 Step 5: Create the Menu File**

* Create a file named `menu.txt` and add the list of available food items along with their prices in rupees, separated by commas.
    

```plaintext
Burger,120
Pizza,250
Salad,180
Soda,40
Pasta,180
Sandwich,150
Coke,50
Fries,100
Ice Cream,120
```

**Step 6: Set Execute Permissions**

* Set execute permissions for the script using the command: `chmod +x restaurant_order.sh`.
    

**Step 8: Run the Script**

* Execute the script using the command: `./restaurant_order.sh`.
    
* Follow the on-screen instructions to place your order.
    
* To finish the order, type "done" when asked for the item name.
    

# **📍 Conclusion:**

By creating a Bash-based restaurant order system, we have successfully automated the process, allowing customers to place their orders seamlessly and receive accurate total bills. The script not only streamlines the restaurant's workflow but also enhances customer satisfaction by reducing waiting times and minimizing errors. By following the step-by-step guide, you can now implement your own automated restaurant order system using Bash scripting! 🍽️🍕🥗🥤

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690656559825/0474ff76-1d75-4ce0-93ea-1194d2444f74.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690893614276/e567a0e4-c76d-4f49-b537-34ca8e727e5d.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")](https://www.youtube.com/@sumanprasad007)