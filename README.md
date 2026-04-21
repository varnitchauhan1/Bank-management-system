# Bank-management-system

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
class BankGUISystem extends JFrame {
 // Data storage (Simulating your BankAccount class)
 private String name = "";
 private int accountNumber = 0;
 private double balance = 0.0;
 // GUI Components
 private JTextField nameField, accField, amountField;
 private JLabel statusLabel, balanceLabel;
 public BankGUISystem() {
 // Window Setup
 setTitle("Bank Management System");
 setSize(400, 450);
 setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
 setLayout(new GridLayout(9, 1, 5, 5));
 // Creating Components
 nameField = new JTextField();
 accField = new JTextField();
 amountField = new JTextField();
 balanceLabel = new JLabel("Balance: $0.0", SwingConstants.CENTER);
 statusLabel = new JLabel("Welcome! Please create an account.", 
SwingConstants.CENTER);
 JButton btnCreate = new JButton("Create Account");
 JButton btnDeposit = new JButton("Deposit");
 JButton btnWithdraw = new JButton("Withdraw");
 // Adding Components to Window
 add(new JLabel(" Name:"));
 add(nameField);
 add(new JLabel(" Account Number:"));
 add(accField);
 add(btnCreate);
 add(new JLabel(" Amount (for Deposit/Withdraw):"));
 add(amountField);
 add(new JPanel() {{
 add(btnDeposit);
 add(btnWithdraw);
 }});
 add(balanceLabel);
 add(statusLabel);
 // Button Actions
 btnCreate.addActionListener(e -> {
 name = nameField.getText();
 try {
 accountNumber = Integer.parseInt(accField.getText());
 balance = 0.0;
 updateDisplay("Account Created for " + name);
 } catch (NumberFormatException ex) {
 statusLabel.setText("Invalid Account Number!");
});
 btnDeposit.addActionListener(e -> {
 try {
 double amt = Double.parseDouble(amountField.getText());
 balance += amt;
 updateDisplay("Deposited: $" + amt);
 } catch (NumberFormatException ex) {
 statusLabel.setText("Enter valid amount!");
 }
 });
 btnWithdraw.addActionListener(e -> {
 try {
 double amt = Double.parseDouble(amountField.getText());
 if (amt <= balance) {
 balance -= amt;
updateDisplay("Withdrew: $" + amt);
 } else {
 statusLabel.setText("Insufficient Balance!");
 }
 } catch (NumberFormatException ex) {
 statusLabel.setText("Enter valid amount!");
 }
 });
 setVisible(true);
 }
 private void updateDisplay(String message) {
 balanceLabel.setText("Balance: $" + balance);
 statusLabel.setText(message);
 amountField.setText("");
 }
 public static void main(String[] args) {
new BankGUISystem();
}
}
