## Build a User Configuration Manager
In this lab, you will build a User Configuration Manager that allows users to manage their settings such as theme, language, and notifications. You will implement functions to add, update, delete, and view user settings.

Objective: Fulfill the user stories below and get all the tests to pass to complete the lab.

User Stories:

You should define a function named add_setting with two parameters representing a dictionary of settings and a tuple containing a key-value pair

add_setting function should:

Convert the key and value to lowercase.
If the key setting exists, return Setting '[key]' already exists! Cannot add a new setting with this name.
If the key setting doesn't exist, add the key-value pair to the given dictionary of settings and return Setting '[key]' added with value '[value]' successfully!.
The messages returned should have the key and value in lowercase.
You should define a function named update_setting with two parameters representing a dictionary of settings and a tuple containing a key-value pair.

update_setting function should:

Convert the key and value to lowercase.
If the key setting exists, update its value in the given dictionary of settings and return: Setting '[key]' updated to '[value]' successfully!
If the key setting doesn't exist, return Setting '[key]' does not exist! Cannot update a non-existing setting.
The messages returned should have the key and value in lowercase.
You should define a function named delete_setting with two parameters representing a dictionary of settings and a key.

delete_setting function should:

Convert the key passed to lowercase.
If the key setting exists, remove the key-value pair from the given dictionary of settings and return Setting '[key]' deleted successfully!
If the key setting does not exist, return Setting not found!
The messages returned should have the key in lowercase.
You should define a function named view_settings with one parameter representing a dictionary of settings.

view_settings function should:

Return No settings available. if the given dictionary of settings is empty.
If the dictionary contains any settings, return a string displaying the settings. The string should start with Current User Settings: followed by the key-value pairs, each on a new line and with the key capitalized. For example, view_settings({'theme': 'dark', 'notifications': 'enabled', 'volume': 'high'}) should return:
Current User Settings:
Theme: dark
Notifications: enabled
Volume: high

For testing the code, you should create a dictionary named test_settings to store some user configuration preferences.

Tests:
Passed:1. You should create a dictionary named test_settings and add some values to it.
Passed:2. You should define a function named add_setting.
Passed:3. The add_setting function should have two parameters.
Passed:4. add_setting should convert the key to lowercase.
Passed:5. add_setting should convert the value to lowercase.
Passed:6. add_setting({'theme': 'light'}, ('THEME', 'dark')) should return the error message Setting 'theme' already exists! Cannot add a new setting with this name..
Passed:7. add_setting({'theme': 'light'}, ('volume', 'high')) should add a new key-value pair and return the success message Setting 'volume' added with value 'high' successfully!.
Passed:8. add_setting should correctly add the given key-value pair to the dictionary.
Passed:9. You should define a function named update_setting.
Passed:10. The update_setting function should have two parameters.
Passed:11. The update_setting function should convert key to lowercase.
Passed:12. The update_setting function should convert value to lowercase.
Passed:13. update_setting({'theme': 'light'}, ('theme', 'dark')) should update an existing key and return the success message Setting 'theme' updated to 'dark' successfully!.
Passed:14. update_setting({'theme': 'light'}, ('volume', 'high')) should return the error message Setting 'volume' does not exist! Cannot update a non-existing setting. when the key doesn't exist.
Passed:15. update_setting should correctly update the given key-value pair in the dictionary.
Passed:16. You should define a function named delete_setting.
Passed:17. The delete_setting function should have two parameters.
Passed:18. delete_setting should convert the key to lowercase.
Passed:19. delete_setting({'theme': 'light'}, 'theme') should remove the existing key and return the success message Setting 'theme' deleted successfully!.
Passed:20. delete_setting should return the error message Setting not found! when the key doesn't exist.
Passed:21. delete_setting should correctly remove the given key from the dictionary.
Passed:22. You should define a function named view_settings.
Passed:23. The view_settings function should have one parameter.
Passed:24. view_settings should return the message No settings available. if the given dictionary is empty.
Passed:25. view_settings should return formatted settings for non-empty dictionary.
Passed:26. view_settings should capitalize the first letter of each setting name.
Passed:27. view_settings should display the correct results and end with a newline character.

code: 
```python
def add_setting(dictionary, tup):
    key = tup[0].lower()
    value = tup[1].lower()
    if key in dictionary:
        return f"Setting '{key}' already exists! Cannot add a new setting with this name."
    else:
        dictionary[key] = value
        return f"Setting '{key}' added with value '{value}' successfully!"

def update_setting(dictionary, tup):
    key = tup[0].lower()
    value = tup[1].lower()
    if not key in dictionary:
        return f"Setting '{key}' does not exist! Cannot update a non-existing setting."
    else:
        dictionary[key] = value
        return f"Setting '{key}' updated to '{value}' successfully!"


def delete_setting(dictionary, key):
    key = key.lower()
    if key not in dictionary:
        return 'Setting not found!'
    else: 
        del dictionary[key]
        return f"Setting '{key}' deleted successfully!"

def view_settings(dictionary):
    if not dictionary:
        return 'No settings available.'
    else: 
        message = 'Current User Settings:\n'
        for items in dictionary: 
            message += items.capitalize() + ': ' + dictionary[items] + '\n'
        return message

test_settings = {'theme': 'dark', 'notifications': 'enabled', 'volume': 'high'}
```




---




## Build a Budget App
In this lab, you will build a simple budget app that tracks spending in different categories and can show the relative spending percentage on a graph.

**Objective:** Fulfill the user stories below and get all the tests to pass to complete the lab.

**User Stories:**
1. You should have a Category class that accepts a name as the argument.
2. The Category class should have an instance attribute ledger that is a list, and contains the list of transactions.
3. The Category class should have the following methods:
    - A deposit method that accepts an amount and an optional description. If no description is given, it should default to an empty string. The method should append an object to the ledger list in the form of {'amount': amount, 'description': description}.
    - A withdraw method that accepts an amount and an optional description (default to an empty string). The method should store in ledger the amount passed in as a negative number, and should return True if the withdrawal succeeded and False otherwise.
    - A get_balance method that returns the current category balance based on ledger.
    - A transfer method that accepts an amount and another Category instance, withdraws the amount with description Transfer to [Destination], deposits it into the other category with description Transfer from [Source], where [Destination] and [Source] should be replaced by the name of destination and source categories. The method should return True when the transfer is successful, and False otherwise.
    - A check_funds method that accepts an amount and returns False if it exceeds the balance or True otherwise. This method must be used by both the withdraw and transfer methods.
4. When a Category object is printed, it should:
    - Display a title line of 30 characters with the category name centered between * characters.
    - List each ledger entry with up to 23 characters of its description left-aligned and the amount right-aligned (two decimal places, max 7 characters).
    - Show a final line Total: [balance], where [balance] should be replaced by the category total.
    
    - Here is an example usage:
    ```bash
    food = Category('Food')
    food.deposit(1000, 'initial deposit')
    food.withdraw(10.15, 'groceries')
    food.withdraw(15.89, 'restaurant and more food for dessert')
    clothing = Category('Clothing')
    food.transfer(50, clothing)
    print(food)
    ```
    - And here is an example of the output:
    ```bash
    *************Food*************
    initial deposit        1000.00
    groceries               -10.15
    restaurant and more foo -15.89
    Transfer to Clothing    -50.00
    Total: 923.96
    ```
    
5. You should have a function outside the Category class named create_spend_chart(categories) that returns a bar-chart string. To build the chart:
    - Start with the title Percentage spent by category.
    - Calculate percentages from withdrawals only and not from deposits. The percentage should be the percentage of the amount spent for each category to the total spent for all categories (rounded down to the nearest 10).
    - Label the y-axis from 100 down to 0 in steps of 10.
    - Use o characters for the bars.
    - Include a horizontal line two spaces past the last bar.
    - Write category names vertically below the bar.
This function will be tested with up to four categories.

Make sure to match the spacing of the example output exactly:
```bash
Percentage spent by category
100|          
 90|          
 80|          
 70|          
 60| o        
 50| o        
 40| o        
 30| o        
 20| o  o     
 10| o  o  o  
  0| o  o  o  
    ----------
     F  C  A  
     o  l  u  
     o  o  t  
     d  t  o  
        h     
        i     
        n     
        g     
```

NOTE: open the browser console with F12 to see a more verbose output of the tests.

Tests:
- Passed:1. The deposit method should create a specific object in the ledger instance variable.
- Passed:2. Calling the deposit method with no description should create a blank description.
- Passed:3. The withdraw method should create a specific object in the ledger instance variable.
Passed:4. Calling the withdraw method with no description should create a blank description.
Passed:5. The withdraw method should return True if the withdrawal took place.
Passed:6. Calling food.deposit(900, 'deposit') and food.withdraw(45.67, 'milk, cereal, eggs, bacon, bread') should return a balance of 854.33.
Passed:7. Calling the transfer method on a category object should create a specific ledger item in that category object.
Passed:8. The transfer method should return True if the transfer took place.
Passed:9. Calling transfer on a category object should reduce the balance in the category object.
Passed:10. The transfer method should increase the balance of the category object passed as its argument.
Passed:11. The transfer method should create a specific ledger item in the category object passed as its argument.
Passed:12. The check_funds method should return False if the amount passed to the method is greater than the category balance.
Passed:13. The check_funds method should return True if the amount passed to the method is not greater than the category balance.
Passed:14. The withdraw method should return False if the withdrawal didn't take place.
Passed:15. The transfer method should return False if the transfer didn't take place.
Passed:16. Printing a Category instance should give a different string representation of the object.
Passed:17. Title at the top of create_spend_chart chart should say Percentage spent by category.
Passed:18. create_spend_chart chart should have correct percentages down the left side.
Passed:19. The height of each bar on the create_spend_chart chart should be rounded down to the nearest 10.
Passed:20. Each line in create_spend_chart chart should have the same length. Bars for different categories should be separated by two spaces, with additional two spaces after the final bar.
Passed:21. create_spend_chart should correctly show horizontal line below the bars. Using three - characters for each category, and in total going two characters past the final bar.
Passed:22. create_spend_chart chart should not have new line character at the end.
Passed:23. create_spend_chart chart should have each category name written vertically below the bar. Each line should have the same length, each category should be separated by two spaces, with additional two spaces after the final category.
Passed:24. create_spend_chart should print a different chart representation. Check that all spacing is exact. Open your browser console with F12 for more details.


### Python Complete Code: 
```python 
class Category:
    def __init__(self, name):
        self.name = name
        self.ledger = []
        self.balance = 0

    def deposit(self, amount, description=''):
        self.balance += amount
        self.ledger.append({
            'amount': amount,
            'description': description
        })

    def withdraw(self, amount, description=''):
        if not self.check_funds(amount):
            return False
        self.balance -= amount
        self.ledger.append({
            'amount': -amount,
            'description': description
        })
        return True

    def get_balance(self):
        return self.balance

    def transfer(self, amount, destination):
        if not self.check_funds(amount):
            return False
        self.withdraw(amount, f"Transfer to {destination.name}")
        destination.deposit(amount, f"Transfer from {self.name}")
        return True

    def check_funds(self, amount):
        return amount <= self.balance

    def __str__(self):
        receipt = self.name.center(30, '*') + '\n'
        for item in self.ledger:
            amount = f"{item['amount']:.2f}"
            receipt += f"{item['description'][:23]:23}{amount:>7}\n"
        receipt += f"Total: {self.balance:.2f}"
        return receipt

def create_spend_chart(categories):
    title = "Percentage spent by category\n"

    spent = []
    for category in categories:
        total = 0
        for item in category.ledger:
            if item["amount"] < 0:
                total += -item["amount"]
        spent.append(total)

    total_spent = sum(spent)

    percentages = []
    for amount in spent:
        percent = int((amount / total_spent) * 100)
        percentages.append(percent - (percent % 10))

    chart = title
    for level in range(100, -1, -10):
        chart += f"{level:>3}| "
        for percent in percentages:
            chart += "o  " if percent >= level else "   "
        chart += "\n"

    chart += "    " + "-" * (len(categories) * 3 + 1) + "\n"

    names = [category.name for category in categories]
    max_len = max(len(name) for name in names)

    for i in range(max_len):
        chart += "     "
        for name in names:
            chart += (name[i] if i < len(name) else " ") + "  "
        chart += "\n"

    return chart.rstrip("\n")

def main():
    food = Category('Food')
    food.deposit(1000, 'initial deposit')
    food.withdraw(10.15, 'groceries')
    food.withdraw(15.89, 'restaurant and more food for dessert')
    clothing = Category('Clothing')
    food.transfer(50, clothing)
    print(food)

if __name__ == '__main__':
    main()
```


