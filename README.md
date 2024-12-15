# raahim
hospital management system 
import java.util.*;

// Patient Class
class Patient {
    int id;
    String name;
    int age;
    String disease;

    Patient(int id, String name, int age, String disease) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.disease = disease;
    }

    @Override
    public String toString() {
        return "ID: " + id + ", Name: " + name + ", Age: " + age + ", Disease: " + disease;
    }
}

// Hospital Management System Class
class HospitalManagement {
    LinkedList<Patient> patients = new LinkedList<>();  // LinkedList for patient records
    PriorityQueue<Patient> appointments = new PriorityQueue<>((a, b) -> a.age - b.age);  // Priority Queue based on age
    HashMap<Integer, Patient> patientMap = new HashMap<>();  // HashMap for fast searching

    // Add new patient
    public void addPatient(int id, String name, int age, String disease) {
        Patient newPatient = new Patient(id, name, age, disease);
        patients.add(newPatient);
        appointments.add(newPatient);
        patientMap.put(id, newPatient);
        System.out.println("Patient added successfully!");
    }

    // Search for a patient by ID
    public void searchPatient(int id) {
        if (patientMap.containsKey(id)) {
            System.out.println("Patient Found: " + patientMap.get(id));
        } else {
            System.out.println("Patient with ID " + id + " not found.");
        }
    }

    // Schedule the next appointment
    public void scheduleNextAppointment() {
        if (!appointments.isEmpty()) {
            Patient next = appointments.poll();
            System.out.println("Next Appointment: " + next);
        } else {
            System.out.println("No appointments pending.");
        }
    }

    // Display all patients
    public void displayPatients() {
        System.out.println("---- Patient List ----");
        for (Patient p : patients) {
            System.out.println(p);
        }
    }
}

// Main Class
public class Main {
    public static void main(String[] args) {
        HospitalManagement hm = new HospitalManagement();
        Scanner sc = new Scanner(System.in);

        while (true) {
            System.out.println("\n--- Hospital Management Menu ---");
            System.out.println("1. Add Patient");
            System.out.println("2. Search Patient");
            System.out.println("3. Schedule Next Appointment");
            System.out.println("4. Display All Patients");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter ID: ");
                    int id = sc.nextInt();
                    sc.nextLine();  // Consume the newline
                    System.out.print("Enter Name: ");
                    String name = sc.nextLine();
                    System.out.print("Enter Age: ");
                    int age = sc.nextInt();
                    sc.nextLine();  // Consume the newline
                    System.out.print("Enter Disease: ");
                    String disease = sc.nextLine();
                    hm.addPatient(id, name, age, disease);
                    break;
                case 2:
                    System.out.print("Enter Patient ID to Search: ");
                    int searchId = sc.nextInt();
                    hm.searchPatient(searchId);
                    break;
                case 3:
                    hm.scheduleNextAppointment();
                    break;
                case 4:
                    hm.displayPatients();
                    break;
                case 5:
                    System.out.println("Exiting... Thank you!");
                    sc.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid choice! Try again.");
            }
        }
    }
}
