package inheritance1;

import java.util.Scanner;

public class oop3
 {
    public static void main(String[] args) {
        int choice, cont;
        Scanner scanner = new Scanner(System.in);

        do {
            System.out.println("PAYROLL");
            System.out.print("1. Programmer\n2. Assistant Professor\n3. Associate Professor\n4. Professor\n");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); 
            switch (choice) {
                case 1:
                    new Programmer().processEmployee(scanner);
                    break;
                case 2:
                    new AssistantProfessor().processEmployee(scanner);
                    break;
                case 3:
                    new AssociateProfessor().processEmployee(scanner);
                    break;
                case 4:
                    new ProfessorImpl().processEmployee(scanner);
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
            System.out.print("Enter 0 to quit and 1 to continue: ");
            cont = scanner.nextInt();
            scanner.nextLine(); 
        } while (cont == 1);

        scanner.close();
    }
}

class Employee {
    int empid;
    long mobile;
    String name, address, mailid;

    void getData(Scanner scanner) {
        System.out.print("Enter Name of the Employee: ");
        name = scanner.nextLine();
        System.out.print("Enter mailId: ");
        mailid = scanner.nextLine();
        System.out.print("Enter Address of the Employee: ");
        address = scanner.nextLine();
        System.out.print("Enter the employee id: ");
        empid = scanner.nextInt();
        System.out.print("Enter Mobile Number: ");
        mobile = scanner.nextLong();
        scanner.nextLine(); 
    }

    void display() {
        System.out.println("Employee Name: " + name);
        System.out.println("Employee Id: " + empid);
        System.out.println("Mail Id: " + mailid);
        System.out.println("Address: " + address);
        System.out.println("Mobile Number: " + mobile);
    }
}

abstract class Professor extends Employee {
    double basicPay, da, hra, pf, club, net, gross;

    void getBasicPay(Scanner scanner) {
        System.out.print("Enter basic pay: ");
        basicPay = scanner.nextDouble();
    }

    void calculate() {
        da = 0.97 * basicPay;
        hra = 0.10 * basicPay;
        pf = 0.12 * basicPay;
        club = 0.1 * basicPay;
        gross = basicPay + da + hra;
        net = gross - pf - club;
    }

    void processEmployee(Scanner scanner) {
        getData(scanner);
        getBasicPay(scanner);
        calculate();
        display(); 
        displayPaySlip();
    }

    void displayPaySlip() {
        System.out.println("*****************************");
        System.out.println("PAY SLIP FOR " + this.getClass().getSimpleName());
        System.out.println("*****************************");
        System.out.println("Basic Pay: Rs." + basicPay);
        System.out.println("DA: Rs." + da);
        System.out.println("HRA: Rs." + hra);
        System.out.println("PF: Rs." + pf);
        System.out.println("CLUB: Rs." + club);
        System.out.println("GROSS PAY: Rs." + gross);
        System.out.println("NET PAY: Rs. " + net);
    }
}

class Programmer extends Professor {
}

class AssistantProfessor extends Professor {
}

class AssociateProfessor extends Professor {
}

class ProfessorImpl extends Professor {
}
