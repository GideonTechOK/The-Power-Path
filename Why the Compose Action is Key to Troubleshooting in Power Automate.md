## Why the Compose Action is Key to Troubleshooting in Power Automate

The **Compose** action in Power Automate is an invaluable tool for troubleshooting and debugging flows. Compose allows you to display, inspect, and manipulate data without affecting the main process flow, making it essential for diagnosing issues, testing expressions, and verifying outputs. Here’s why it’s key and how to use it effectively with an example.

### Benefits of Using the Compose Action

1. **Inspect Data at Key Stages**: The Compose action displays data at any point in your flow, helping you see what’s actually being passed between actions.
2. **Test Expressions and Calculations**: Use Compose to test formulas and expressions. This can help avoid errors like `InvalidTemplate` by letting you validate logic before using it in other actions.
3. **Avoid Unnecessary Changes**: Unlike `Set Variable`, which alters the flow state, Compose simply displays data, allowing you to debug without changing the flow’s core data.

### Example: Troubleshooting with Compose

Let’s say you’re working on a flow that processes an order and calculates a discount based on order value. You encounter an issue where the flow unexpectedly fails, and you suspect it’s due to a calculation error. Here’s how you can use Compose to troubleshoot.

#### Initial Flow Logic

The original flow steps might look like this:

1. **Trigger**: When an order is received, retrieve the order amount.
2. **Condition**: Check if the order amount is over $100 to apply a discount.
3. **Action**: Calculate the discount (10% of the order amount).
4. **Action**: Send the final order amount to a database or email.

#### Troubleshooting with Compose

1. **Add a Compose Action to Inspect Order Amount**: After retrieving the order, add a **Compose** action to display the raw order amount.

   ```markdown
   1. Add Compose action after retrieving the order amount.
   2. In the **Inputs** field of Compose, set the value as the `Order Amount` variable.
   ```

2. **Add Compose to Test Discount Calculation**: Before applying the discount calculation, use Compose to test the formula and verify that it’s working as expected.

   ```markdown
   1. Add another Compose action before the discount calculation.
   2. Use an expression like this in the **Inputs** field: `float(OrderAmount) * 0.1`
   3. Run the flow and check the result of this Compose action in the run history.
   ```

3. **Review Output in Run History**: After running the flow, check the run history. Each Compose action will display its calculated output, helping you confirm if the order amount and discount calculation are correct.

#### Example of Expressions in Compose

Suppose your order data is stored in a variable called `OrderAmount`, and you want to display the discounted price. You could use Compose like this:

```markdown
Add a Compose action and use the following expression in the **Inputs** field:

`sub(float(OrderAmount), mul(float(OrderAmount), 0.1))`

This expression subtracts a 10% discount from the `OrderAmount`. Run the flow and check the Compose action’s output to ensure the calculation is correct.
```

### Summary

Using Compose actions throughout a flow helps you understand what’s happening at each stage. It’s like adding checkpoints that show you the exact data, making it much easier to identify issues, test expressions, and fix any unexpected behaviors. When troubleshooting Power Automate flows, Compose is a key action to include, especially when working with complex data transformations or conditions.
