# projects
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package todolistapp;

/**
 *
 * @author sanelisiwe
 */
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;

public class ToDoListApp {
    private JFrame frame;
    private JPanel panel;
    private JTextField taskInputField;
    private JButton addButton;
    private JButton removeButton;
    private java.util.List<JCheckBox> tasks;

    public ToDoListApp() {
        // Set up the frame
        frame = new JFrame("To-Do List");
        panel = new JPanel();
        taskInputField = new JTextField(20);  // Input field for the task
        addButton = new JButton("Add Task");
        removeButton = new JButton("Remove Completed Tasks");
        tasks = new ArrayList<>();

        panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS));

        panel.add(taskInputField);
        panel.add(addButton);
        panel.add(removeButton);

        // Add task button action listener
        addButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String taskText = taskInputField.getText();  // Get text from input field
                if (!taskText.isEmpty()) {  // Check if input is not empty
                    JCheckBox task = new JCheckBox(taskText);  // Create new task
                    tasks.add(task);
                    panel.add(task);
                    taskInputField.setText("");  // Clear input field after adding task
                    frame.revalidate();
                    frame.repaint();
                }
            }
        });

        // Remove completed tasks button action listener
        removeButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                java.util.List<JCheckBox> tasksToRemove = new ArrayList<>();
                for (JCheckBox task : tasks) {
                    if (task.isSelected()) {
                        panel.remove(task);  // Remove task from panel
                        tasksToRemove.add(task);
                    }
                }
                tasks.removeAll(tasksToRemove);  // Remove tasks from the list
                frame.revalidate();
                frame.repaint();
            }
        });

        frame.add(panel);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(300, 400);
        frame.setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new ToDoListApp();
            }
        });
    }
}

                
