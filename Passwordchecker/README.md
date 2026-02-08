# Passwordchecker

/**
 *
 * This application checks password.
 * A password should have minimum 8 character long.
 * A password should have lower and upper case letters.
 * A password should have number(0-9)and special character.
 * The system should say whether a password is weak or moderate or strong.
 */
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Password_checker extends JFrame {

    private JTextField passwordField;
    private JLabel resultLabel;

    public static void main(String[] args) {
        Password_checker frame = new Password_checker();
        frame.setSize(600, 250);
        frame.setTitle("Password Strength Checker");
        frame.createGUI();
        frame.setVisible(true);
    }

    // Method to create GUI
    private void createGUI() {
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        Container window = getContentPane();
        window.setLayout(new FlowLayout());

        // Password input field
        passwordField = new JTextField(20);
        window.add(new JLabel("Enter Password:"));
        window.add(passwordField);

        // Button to check password
        JButton checkButton = new JButton("Check Strength");
        window.add(checkButton);

        // Label to show result
        resultLabel = new JLabel(" ");
        window.add(resultLabel);

        // Button click action
        checkButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String password = passwordField.getText();
                checkPasswordStrength(password);
            }
        });
    }

    // Method to check password strength
    private void checkPasswordStrength(String password) {

        int score = 0;

        // Check length
        if (password.length() >= 8) {
            score++;
        }

        // Check for lowercase letter
        if (password.matches(".*[a-z].*")) {
            score++;
        }

        // Check for uppercase letter
        if (password.matches(".*[A-Z].*")) {
            score++;
        }

        // Check for number
        if (password.matches(".*[0-9].*")) {
            score++;
        }

        // Check for special character
        if (password.matches(".*[^a-zA-Z0-9].*")) {
            score++;
        }

        // Decide strength
        if (score <= 2) {
            resultLabel.setText("Password Strength: WEAK");
        } else if (score <= 4) {
            resultLabel.setText("Password Strength: MODERATE");
        } else {
            resultLabel.setText("Password Strength: STRONG");
        }