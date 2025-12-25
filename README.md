# BUDGET-BUDDY
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.stage.Stage;
import javafx.scene.paint.Color;

public class BudgetBuddyApp extends Application {

    double totalExpenses = 0;
    double budgetLimit = 0;

    
    public void start(Stage stage) {

        // For  Labels
        Label budgetLabel = new Label("Enter Your Monthly Budget:");
        Label expenseLabel = new Label("Enter Your Expense:");
        Label totalLabel = new Label("Total Expenses: ₹0.0");
        Label alertLabel = new Label("");

        // For Text fields user input

        TextField budgetInput = new TextField();
        TextField expenseInput = new TextField();

        //For Buttons
        Button setBudgetBtn = new Button("Set Budget");
        Button addExpenseBtn = new Button("Add Expense");
        Button resetBtn = new Button("Reset");

        // For Set Budget Button Action
        setBudgetBtn.setOnAction(e -> {
            try {
                budgetLimit = Double.parseDouble(budgetInput.getText());
                alertLabel.setText("Budget set to: ₹" + budgetLimit);
                alertLabel.setTextFill(Color.GREEN);
            } catch (NumberFormatException ex) {
                alertLabel.setText("Please enter a valid number!");
                alertLabel.setTextFill(Color.RED);
            }
        });

        // For  Add Expense Button Action
        addExpenseBtn.setOnAction(e -> {
            try {
                double expense = Double.parseDouble(expenseInput.getText());
                totalExpenses += expense;
                totalLabel.setText("Total Expenses: ₹" + totalExpenses);

                if (totalExpenses > budgetLimit && budgetLimit > 0) {
                    alertLabel.setText("⚠️ You exceeded your budget!");
                    alertLabel.setTextFill(Color.RED);
                } else if (budgetLimit == 0) {
                    alertLabel.setText("Please set a budget first!");
                    alertLabel.setTextFill(Color.ORANGE);
                } else {
                    alertLabel.setText("Expense added successfully ✅");
                    alertLabel.setTextFill(Color.GREEN);
                }

                expenseInput.clear();

            } catch (NumberFormatException ex) {
                alertLabel.setText("Enter valid expense amount!");
                alertLabel.setTextFill(Color.RED);
            }
        });

        // For Reset Button Action

        resetBtn.setOnAction(e -> {
            totalExpenses = 0;
            budgetLimit = 0;
            budgetInput.clear();
            expenseInput.clear();
            totalLabel.setText("Total Expenses: ₹0.0");
            alertLabel.setText("All data cleared.");
            alertLabel.setTextFill(Color.BLACK);
        });

        // For Layout

        VBox layout = new VBox(10);
        layout.setStyle("-fx-padding: 20; -fx-font-size: 14;");
        layout.getChildren().addAll(
                budgetLabel, budgetInput, setBudgetBtn,
                expenseLabel, expenseInput, addExpenseBtn,
                totalLabel, alertLabel, resetBtn
        );

        // For Scene and Stage

        Scene scene = new Scene(layout, 350, 400);
        stage.setTitle("💰 Budget Buddy");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}