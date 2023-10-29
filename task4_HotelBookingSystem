import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import java.util.List;

public class HotelBookingSystemGUI {
    private List<City> cities;
    private List<User> users;
    private User currentUser;

    private JFrame frame;
    private JPanel contentPanel;
    private City selectedCity;
    private Hotel selectedHotel;

    public HotelBookingSystemGUI() {
        cities = new ArrayList<>();
        users = new ArrayList<>();

        // Create cities
        City bangalore = new City("Bangalore");
        City hyderabad = new City("Hyderabad");
        City chennai = new City("Chennai");
        City mumbai = new City("Mumbai");

        // Add hotels to cities
        bangalore.addHotel(new Hotel("Royal Resorts", "AC", 3500));
        bangalore.addHotel(new Hotel("The Grand Hotel", "Non-AC", 2500));
        hyderabad.addHotel(new Hotel("New Convention Hotel", "AC", 4000));
        hyderabad.addHotel(new Hotel("Royal Resorts", "Non-AC", 3000));
        chennai.addHotel(new Hotel("The Grand Hotel", "AC", 3800));
        chennai.addHotel(new Hotel("New Convention Hotel", "Non-AC", 2800));
        mumbai.addHotel(new Hotel("The Grand Hotel", "AC", 4500));
        mumbai.addHotel(new Hotel("Royal Resorts", "Non-AC", 3500));

        cities.add(bangalore);
        cities.add(hyderabad);
        cities.add(chennai);
        cities.add(mumbai);

        frame = new JFrame("Hotel Booking System");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 300);
        frame.setLayout(new FlowLayout());

        contentPanel = new JPanel();
        frame.add(contentPanel);

        createLoginUI();
    }

    private void createLoginUI() {
        contentPanel.removeAll();
        contentPanel.setLayout(new FlowLayout());

        JLabel usernameLabel = new JLabel("Username: ");
        JLabel passwordLabel = new JLabel("Password: ");
        JTextField usernameField = new JTextField(10);
        JPasswordField passwordField = new JPasswordField(10);
        JButton loginButton = new JButton("Login");
        JButton createAccountButton = new JButton("Create Account");

        loginButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());

                if (loginUser(username, password)) {
                    createCitySelectionUI();
                } else {
                    JOptionPane.showMessageDialog(null, "Invalid username or password.");
                }
            }
        });

        createAccountButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                createAccountUI();
            }
        });

        contentPanel.add(usernameLabel);
        contentPanel.add(usernameField);
        contentPanel.add(passwordLabel);
        contentPanel.add(passwordField);
        contentPanel.add(loginButton);
        contentPanel.add(createAccountButton);

        frame.revalidate();
        frame.repaint();
        frame.setVisible(true);
    }

    private void createAccountUI() {
        String newUsername = JOptionPane.showInputDialog(null, "Enter a new username:");
        if (newUsername != null && !newUsername.trim().isEmpty()) {
            String newPassword = JOptionPane.showInputDialog(null, "Enter a password:");
            if (newPassword != null && !newPassword.trim().isEmpty()) {
                User newUser = new User(newUsername, newPassword);
                users.add(newUser);
                JOptionPane.showMessageDialog(null, "Account created successfully.");
            } else {
                JOptionPane.showMessageDialog(null, "Invalid password.");
            }
        } else {
            JOptionPane.showMessageDialog(null, "Invalid username.");
        }
    }

    private void createCitySelectionUI() {
        contentPanel.removeAll();
        contentPanel.setLayout(new FlowLayout());

        JLabel selectCityLabel = new JLabel("Select a City: ");
        JComboBox<String> cityComboBox = new JComboBox<>();
        for (City city : cities) {
            cityComboBox.addItem(city.getName());
        }

        JButton selectCityButton = new JButton("Select City");

        selectCityButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String selectedCityName = (String) cityComboBox.getSelectedItem();
                selectedCity = getCityByName(selectedCityName);
                createHotelSelectionUI();
            }
        });

        contentPanel.add(selectCityLabel);
        contentPanel.add(cityComboBox);
        contentPanel.add(selectCityButton);

        frame.revalidate();
        frame.repaint();
    }

    private void createHotelSelectionUI() {
        contentPanel.removeAll();
        contentPanel.setLayout(new FlowLayout());

        JLabel selectHotelLabel = new JLabel("Select a Hotel: ");
        JComboBox<String> hotelComboBox = new JComboBox<>();
        for (Hotel hotel : selectedCity.getHotels()) {
            hotelComboBox.addItem(hotel.getName());
        }

        JButton selectHotelButton = new JButton("Select Hotel");

        selectHotelButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String selectedHotelName = (String) hotelComboBox.getSelectedItem();
                selectedHotel = getHotelByName(selectedHotelName);
                createBookingUI();
            }
        });

        contentPanel.add(selectHotelLabel);
        contentPanel.add(hotelComboBox);
        contentPanel.add(selectHotelButton);

        frame.revalidate();
        frame.repaint();
    }

    private void createBookingUI() {
        contentPanel.removeAll();
        contentPanel.setLayout(new FlowLayout());

        JButton viewRoomsButton = new JButton("View Available Rooms");
        JButton bookRoomButton = new JButton("Book a Room");
        JButton checkOutButton = new JButton("Check Out");
        JButton logoutButton = new JButton("Logout");

        viewRoomsButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                StringBuilder availableRooms = new StringBuilder("Available Rooms at " + selectedHotel.getName() + ":\n");
                for (Room room : selectedHotel.getRooms()) {
                    if (room.isAvailable()) {
                        availableRooms.append("Room ").append(room.getRoomNumber())
                                .append(" (Type: ").append(room.getRoomType())
                                .append(", Price: ₹").append(room.getPrice()) // Use ₹ symbol for Indian Rupees
                                .append("\n");
                    }
                }
                JOptionPane.showMessageDialog(null, availableRooms.toString());
            }
        });

        bookRoomButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String roomNumberStr = JOptionPane.showInputDialog(null, "Enter the room number you want to book:");
                if (roomNumberStr != null) {
                    try {
                        int roomNumber = Integer.parseInt(roomNumberStr);
                        if (bookRoom(roomNumber)) {
                            JOptionPane.showMessageDialog(null, "Room " + roomNumber + " booked successfully.");
                        } else {
                            JOptionPane.showMessageDialog(null, "Room " + roomNumber + " is not available.");
                        }
                    } catch (NumberFormatException ex) {
                        JOptionPane.showMessageDialog(null, "Invalid room number.");
                    }
                }
            }
        });

        checkOutButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String roomNumberStr = JOptionPane.showInputDialog(null, "Enter the room number you want to check out from:");
                if (roomNumberStr != null) {
                    try {
                        int roomNumber = Integer.parseInt(roomNumberStr);
                        if (checkOutRoom(roomNumber)) {
                            JOptionPane.showMessageDialog(null, "Room " + roomNumber + " checked out successfully.");
                        } else {
                            JOptionPane.showMessageDialog(null, "Room " + roomNumber + " is not booked.");
                        }
                    } catch (NumberFormatException ex) {
                        JOptionPane.showMessageDialog(null, "Invalid room number.");
                    }
                }
            }
        });
        logoutButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                currentUser = null;
                createLoginUI();
            }
        });

        contentPanel.add(viewRoomsButton);
        contentPanel.add(bookRoomButton);
        contentPanel.add(checkOutButton);
        contentPanel.add(logoutButton);
        frame.revalidate();
        frame.repaint();
    }

    private boolean bookRoom(int roomNumber) {
        for (Room room : selectedHotel.getRooms()) {
            if (room.getRoomNumber() == roomNumber && room.isAvailable()) {
                room.book();
                return true;
            }
        }
        return false;
    }

    private boolean checkOutRoom(int roomNumber) {
        for (Room room : selectedHotel.getRooms()) {
            if (room.getRoomNumber() == roomNumber && !room.isAvailable()) {
                room.checkOut();
                return true;
            }
        }
        return false;
    }

    private boolean loginUser(String username, String password) {
        for (User user : users) {
            if (user.getUsername().equals(username) && user.getPassword().equals(password)) {
                currentUser = user;
                return true;
            }
        }
        return false;
    }

    private City getCityByName(String cityName) {
        for (City city : cities) {
            if (city.getName().equals(cityName)) {
                return city;
            }
        }
        return null;
    }

    private Hotel getHotelByName(String hotelName) {
        for (Hotel hotel : selectedCity.getHotels()) {
            if (hotel.getName().equals(hotelName)) {
                return hotel;
            }
        }
        return null;
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new HotelBookingSystemGUI());
    }

    private static class Room {
        private int roomNumber;
        private boolean isAvailable;
        private String roomType;
        private double price;

        public Room(int roomNumber, String roomType, double price) {
            this.roomNumber = roomNumber;
            this.isAvailable = true;
            this.roomType = roomType;
            this.price = price;
        }

        public int getRoomNumber() {
            return roomNumber;
        }

        public boolean isAvailable() {
            return isAvailable;
        }

        public void book() {
            isAvailable = false;
        }

        public void checkOut() {
            isAvailable = true;
        }

        public String getRoomType() {
            return roomType;
        }

        public double getPrice() {
            return price;
        }
    }

    private static class User {
        private String username;
        private String password;

        public User(String username, String password) {
            this.username = username;
            this.password = password;
        }

        public String getUsername() {
            return username;
        }

        public String getPassword() {
            return password;
        }
    }

    private static class Hotel {
        private String name;
        private String roomType;
        private double price;
        private List<Room> rooms;

        public Hotel(String name, String roomType, double price) {
            this.name = name;
            this.roomType = roomType;
            this.price = price;
            rooms = new ArrayList<>();
            for (int i = 1; i <= 10; i++) {
                rooms.add(new Room(i, roomType, price));
            }
        }

        public String getName() {
            return name;
        }

        public List<Room> getRooms() {
            return rooms;
        }
    }

    private static class City {
        private String name;
        private List<Hotel> hotels;

        public City(String name) {
            this.name = name;
            hotels = new ArrayList<>();
        }

        public void addHotel(Hotel hotel) {
            hotels.add(hotel);
        }

        public String getName() {
            return name;
        }

        public List<Hotel> getHotels() {
            return hotels;
        }
    }
}
