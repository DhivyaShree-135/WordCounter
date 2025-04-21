import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

class WordCounter1 extends JFrame {
    private JTextArea textArea;
    private JButton countButton;
    private JTextArea resultArea;
    private JComboBox<String> optionBox;

    public WordCounter1() {
        setTitle("Word Counter");
        setSize(600, 450);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // Input Area
        textArea = new JTextArea(10, 40);
        textArea.setLineWrap(true);
        textArea.setWrapStyleWord(true);
        JScrollPane scrollPane = new JScrollPane(textArea);
        add(scrollPane, BorderLayout.CENTER);

        // Control Panel
        JPanel controlPanel = new JPanel();
        controlPanel.setLayout(new FlowLayout());

        // Option Dropdown
        optionBox = new JComboBox<>(new String[]{"Count Words", "Count Characters", "Count Paragraphs"});
        controlPanel.add(new JLabel("Choose an option:"));
        controlPanel.add(optionBox);

        // Count Button
        countButton = new JButton("Calculate");
        countButton.addActionListener(new CountButtonListener());
        controlPanel.add(countButton);

        add(controlPanel, BorderLayout.NORTH);

        // Result Area
        resultArea = new JTextArea(5, 30);
        resultArea.setEditable(false);
        add(new JScrollPane(resultArea), BorderLayout.SOUTH);

        setVisible(true);
    }

    private class CountButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            new Thread(() -> {
                try {
                    String text = textArea.getText();

                    if (text == null || text.trim().isEmpty()) {
                        throw new IllegalArgumentException("Please enter some text.");
                    }

                    String option = (String) optionBox.getSelectedItem();
                    String result = "";

                    switch (option) {
                        case "Count Words":
                            result = "Word Count: " + countWords(text);
                            break;
                        case "Count Characters":
                            result = "Character Count: " + text.length();
                            break;
                        case "Count Paragraphs":
                            result = "Paragraph Count: " + countParagraphs(text);
                            break;
                        default:
                            result = "Invalid option.";
                    }

                    final String output = result;
                    SwingUtilities.invokeLater(() -> resultArea.setText(output));

                } catch (Exception ex) {
                    SwingUtilities.invokeLater(() ->
                        JOptionPane.showMessageDialog(
                            WordCounter.this,
                            "Error: " + ex.getMessage(),
                            "Error",
                            JOptionPane.ERROR_MESSAGE
                        )
                    );
                }
            }).start();
        }

        private int countWords(String text) {
            String[] words = text.trim().split("\\s+");
            return words.length;
        }

        private int countParagraphs(String text) {
            String[] paragraphs = text.trim().split("\\n+");
            return paragraphs.length;
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(WordCounter1::new);
    }
}
