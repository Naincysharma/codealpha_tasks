# codealpha_tasks
import java.awt.*;
import java.util.HashMap;
import javax.swing.*;

public class AIChatBotGUI extends JFrame {

    private JTextArea chatArea;
    private JTextField inputField;
    private JButton sendButton;
    private HashMap<String, String> responses;

    public AIChatBotGUI() {
        setTitle("💬 AI ChatBot");
        setSize(500, 500);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // Chat area
        chatArea = new JTextArea();
        chatArea.setEditable(false);
        chatArea.setFont(new Font("Segoe UI", Font.PLAIN, 16));
        chatArea.setBackground(new Color(245, 245, 245));
        chatArea.setForeground(Color.DARK_GRAY);

        JScrollPane scrollPane = new JScrollPane(chatArea);
        add(scrollPane, BorderLayout.CENTER);

        // Input panel
        JPanel inputPanel = new JPanel();
        inputPanel.setLayout(new BorderLayout());

        inputField = new JTextField();
        inputField.setFont(new Font("Segoe UI", Font.PLAIN, 16));
        inputPanel.add(inputField, BorderLayout.CENTER);

        sendButton = new JButton("Send");
        sendButton.setFont(new Font("Segoe UI", Font.BOLD, 16));
        sendButton.setBackground(new Color(59, 89, 182));
        sendButton.setForeground(Color.WHITE);
        inputPanel.add(sendButton, BorderLayout.EAST);

        add(inputPanel, BorderLayout.SOUTH);

        // Predefined responses
        responses = new HashMap<>();
        addResponses();

        // Send message on button click
        sendButton.addActionListener(e -> sendMessage());

        // Send message on Enter key
        inputField.addActionListener(e -> sendMessage());

        setVisible(true);
    }

    private void sendMessage() {
        String input = inputField.getText().toLowerCase().trim();
        if (input.isEmpty()) return;

        chatArea.append("🧑 You: " + input + "\n");

        boolean found = false;
        for (String key : responses.keySet()) {
            if (input.contains(key)) {
                chatArea.append("🤖 Bot: " + responses.get(key) + "\n\n");
                found = true;
                break;
            }
        }

        if (!found) {
            chatArea.append("🤖 Bot: Sorry, I didn't understand that.\n\n");
        }

        inputField.setText("");
    }

    private void addResponses() {
        // Greetings
        responses.put("hello", "Hello! How can I assist you today?");
        responses.put("hi", "Hi there! Ask me anything.");
        responses.put("how are you", "I'm just a bot, but I'm doing great! 😄");
        responses.put("what is your name", "I'm AI ChatBot, your virtual assistant.");
        responses.put("bye", "Goodbye! Have a great day.");
        responses.put("thanks", "You're welcome! 😊");

        // Java & OOP
        responses.put("what is java", "Java is a popular object-oriented programming language used for building applications.");
        responses.put("what is oop", "OOP stands for Object-Oriented Programming. It includes concepts like classes, objects, inheritance, and polymorphism.");
        responses.put("what is inheritance", "Inheritance allows one class to acquire properties and methods of another class.");
        responses.put("what is polymorphism", "Polymorphism means one method can have many forms. It's a core concept in OOP.");
        responses.put("what is encapsulation", "Encapsulation is the concept of wrapping data and methods into a single unit called a class.");
        responses.put("what is abstraction", "Abstraction means hiding internal details and showing only essential features.");

        // General Knowledge
        responses.put("ipl stands for", "IPL stands for Indian Premier League.");
        responses.put("who is prime minister of india", "As of now, the Prime Minister of India is Narendra Modi.");
        responses.put("what is computer", "A computer is an electronic device that processes data and performs tasks.");
        responses.put("who is the president of india", "As of now, the President of India is Droupadi Murmu.");
        responses.put("what is ai", "AI stands for Artificial Intelligence — the simulation of human intelligence by machines.");

        // Fun
        responses.put("how is the weather", "I'm not connected to the internet, so I can't tell real-time weather.");
        responses.put("tell me a joke", "Why don’t scientists trust atoms? Because they make up everything! 😂");
        responses.put("what is your job", "My job is to help you with your questions and make your life easier.");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(AIChatBotGUI::new);
    }
}
