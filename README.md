# ATM_Interface

import java.text.SimpleDateFormat;
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;
import java.util.Scanner;
import javax.lang.model.util.ElementScanner14;

public class ATM_Interface {

    public static void main(String[] args) {
        // Account details
        String accname = "Ankita Patil";
        String branchname = "Karad";
        String branchaddress = "Vidhyanagar, Karad";
        String branchIFSC = "KRD52348";

        int accnumber = 353535;
        int password = 1234;
        int balance = 0;
        int minbal = 1000;
        boolean flag = true;
        boolean flagb = true;
        boolean flagc = true;
        int paper = 0;
        int attempt = 5;
        int currattempt = 0;

        LocalDate date = LocalDate.now();
        // String dateStr = Datetime.format(DateTimeFormatter.ofPattern("dd-MMM-yyyy"));
        // System.out.println(dateStr);
        System.out.println("current: " + date);

        LocalTime time = LocalTime.now();
        // String timeStr = Datetime.format(DateTimeFormatter.ofPattern("hh:mm:ss"));
        System.out.println("current time: " + time);

        ArrayList<String> transaction = new ArrayList<String>();

        Scanner sc = new Scanner(System.in);

        while (currattempt < attempt) {
            System.out.println("Enter your pin");
            int pass = sc.nextInt();
            if (pass == password) {
                System.out.println("Do you want Paper receipt");
                System.out.println("1. YES");
                System.out.println("2. NO");
                paper = sc.nextInt();
                break;
            } else
                System.out.println("You have entered wrong PIN");
            currattempt = currattempt + 1;
        }

        if (currattempt < 5) // Executing the main task if users enters correct password within limited
                             // attempts
        {
            while (flag == true) {
                System.out.println("\n");
                System.out.println("1. Transaction History");
                System.out.println("2. Withdraw");
                System.out.println("3. Deposit");
                System.out.println("4. Transfer");
                System.out.println("5. Quit");
                System.out.println("6. Change Password");

                System.out.println("What would to like to do now");
                int option = sc.nextInt();

                switch (option) {
                    case 1: {
                        System.out.println("Your Transaction History");
                        for (String q : transaction) {
                            System.out.println(q);
                        }
                        break;

                    }
                    case 2: {
                        while (true) {
                            System.out.println("Enter the withdrawl amount");
                            int withdraw = sc.nextInt();
                            if ((withdraw % 10) == 0) {
                                if (withdraw <= balance) {
                                    if ((balance - withdraw) < 1000) {
                                        System.out.println("Minimum balance has to Rs.1000");

                                    } else {
                                        balance = balance - withdraw;
                                        String sf2 = String.format("You have Successfully withdrawl Rs. %d", withdraw);
                                        String sf3 = String.format("Your balance is Rs. %d", balance);
                                        System.out.println(sf2);
                                        System.out.println(sf3);

                                        String wt = String.format("Withdrawl  Rs. %d", withdraw);
                                        transaction.add(wt);
                                        break;
                                    }
                                } else {
                                    System.out.println("Insufficient balance");

                                }
                            } else
                                System.out.println("Enter the withdraw amount in multiples of 100");
                        }
                        break;
                    }

                    case 3: {
                        while (true) {
                            System.out.println("Enter the deposit amount");
                            int deposit = sc.nextInt();
                            if ((deposit % 10) == 0) {
                                balance = balance + deposit;
                                String sf1 = String.format("You have Successfully deposited Rs. %d", deposit);
                                String sf4 = String.format("Your balance is Rs. %d", balance);
                                System.out.println(sf1);
                                System.out.println(sf4);

                                String dp = String.format("Deposit  Rs. %d", deposit);
                                transaction.add(dp);
                                break;
                            } else {
                                System.out.println("Enter the amount in multiples of 100");
                            }
                        }
                        break;
                    }

                    case 4: {
                        while (true) {
                            System.out.println("Enter the account number of the beneficiary");
                            int accno = sc.nextInt();
                            System.out.println("Enter the IFSC code of the bank of the beneficiary");
                            String ifsc = sc.next();
                            System.out.println(accno);
                            System.out.println("Please confirm the account number of the beneficiary");
                            System.out.println("1. Correct");
                            System.out.println("2. Incorrect");

                            int conf = sc.nextInt();
                            if (conf == 1) {
                                System.out.println("Enter the amount you want to transfer");
                                int transfamount = sc.nextInt();
                                if ((transfamount % 10) == 0) {
                                    if (transfamount <= balance) {
                                        if ((balance - transfamount) < 1000) {
                                            System.out.println("Minimum balance has to Rs 1000");
                                        } else {
                                            balance = balance - transfamount;
                                            String sf2 = String.format("You have successfully transferred Rs %d to %d",
                                                    transfamount, accno);
                                            String sf3 = String.format("Your balance is Rs. %d", balance);
                                            System.out.println(sf2);
                                            System.out.println(sf3);

                                            String tf = String.format("Transfer - Rs. %d", transfamount);
                                            transaction.add(tf);
                                            break;
                                        }
                                    } else {
                                        System.out.println("Insufficient balance");
                                    }
                                } else
                                    System.out.println("Enter the amount in multiple of 100");
                            } else

                                System.out.println("You entered incorrect account number");
                        }
                        break;
                    }

                    case 5: {
                        System.out.println("Thank you for banking with us");
                        flag = false;
                        break;
                    }

                    case 6: {
                        System.out.println("Enter your new pin");
                        int newpin = sc.nextInt();
                        password = newpin;
                        System.out.println("Do not share pin with anyone");
                        System.out.println("You have successfully changed your password");
                        transaction.add("Changed password");
                    }

                    default:
                        System.out.println("Please select an appropriate option");
                        break;
                }

                System.out.println("Would you like to do another transaction");
                System.out.println("1. YES");
                System.out.println("2. NO");
                int df = sc.nextInt();
                if (df == 1)
                    flag = true;
                else
                    flag = false;
            }
            if (paper == 1) {
                String sf6 = String.format("Date: %s" + date);
                String sf7 = String.format("Time: %s" + time);

                String sf9 = String.format("Account Holder Name: %s" + accname);
                String sf10 = String.format("Branch Name: %s" + branchname);
                String sf11 = String.format("Branch Address: %s" + branchaddress);
                String sf12 = String.format("Bank IFSC code: %s" + branchIFSC);
                String sf13 = String.format("Account Number: %d" + accnumber);
                String sf14 = String.format("Your account balance is Rs. %d" + balance);

                System.out.println(sf6);
                System.out.println(sf7);
                System.out.println(sf9);
                System.out.println(sf10);
                System.out.println(sf11);
                System.out.println(sf12);
                System.out.println(sf13);
                System.out.println(sf14);
            }
            System.out.println("Thank you for banking with us");
        } else {
            System.out.println("You have entered wrong pin multiple times");

        }
    }
}
