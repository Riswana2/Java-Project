# Java-Project
package shop.main;

import shop.product.Product;
import shop.product.ProductManager;

import shop.customer.Customer;
import shop.customer.CustomerManager;

import shop.order.Order;
import shop.order.OrderManager;

import java.util.Scanner;

public class ShopApp {

    public static void main(String[] args) {

        Scanner sc =
                new Scanner(System.in);

        ProductManager pm =
                new ProductManager();

        CustomerManager cm =
                new CustomerManager();

        OrderManager om =
                new OrderManager();

        // =========================
        // ADD PRODUCTS
        // =========================

        System.out.println(
                "Enter Number Of Products : ");

        int n = sc.nextInt();

        sc.nextLine();

        for(int i = 1; i <= n; i++) {

            System.out.println(
                    "\nEnter Product ID : ");

            String id =
                    sc.nextLine();

            System.out.println(
                    "Enter Product Name : ");

            String name =
                    sc.nextLine();

            System.out.println(
                    "Enter Product Price : ");

            double price =
                    sc.nextDouble();

            System.out.println(
                    "Enter Product Stock : ");

            int stock =
                    sc.nextInt();

            sc.nextLine();

            System.out.println(
                    "Enter Product Category : ");

            String category =
                    sc.nextLine();

            Product p =
                    new Product(
                            id,
                            name,
                            price,
                            stock);

            pm.addProduct(p);
        }

        // =========================
        // DISPLAY PRODUCTS
        // =========================

        pm.displayAllProducts();

        // =========================
        // CUSTOMER INPUT
        // =========================

        System.out.println(
                "\nEnter Customer ID : ");

        String cid =
                sc.nextLine();

        System.out.println(
                "Enter Customer Name : ");

        String cname =
                sc.nextLine();

        System.out.println(
                "Enter Email : ");

        String email =
                sc.nextLine();

        System.out.println(
                "Enter Phone Number : ");

        String phone =
                sc.nextLine();

        System.out.println(
                "Enter Customer Type "
                        + "(Regular/Premium) : ");

        String type =
                sc.nextLine();

        Customer c1 =
                new Customer(
                        cid,
                        cname,
                        email,
                        phone,
                        type);

        cm.registerCustomer(c1);

        // =========================
        // CREATE ORDER
        // =========================

        Order order1 =
                new Order(
                        "ORD001",
                        c1);

        // =========================
        // BUY PRODUCTS
        // =========================

        String choice = "yes";

        while(choice.equalsIgnoreCase("yes")) {

            System.out.println(
                    "\nEnter Product Number To Buy : ");

            int productNo =
                    sc.nextInt();

            System.out.println(
                    "Enter Quantity : ");

            int qty =
                    sc.nextInt();

            Product selectedProduct =
                    pm.getProduct(productNo - 1);

            order1.addItem(
                    selectedProduct,
                    qty);

            sc.nextLine();

            System.out.println(
                    "\nDo You Want To Buy Another Product? (yes/no)");

            choice =
                    sc.nextLine();
        }

        // =========================
        // PLACE ORDER
        // =========================

        om.placeOrder(order1);

        // =========================
        // GENERATE BILL
        // =========================

        order1.generateBill();

        // =========================
        // DISPLAY ALL ORDERS
        // =========================

        om.displayAllOrders();
    }
}
