# urban-lamp

package libraryDatabase;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.beans.Statement;
import java.sql.Connection;
import java.sql.DriverManager;
import java.awt.Dimension;
import java.awt.FlowLayout;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextField;
import java.sql.PreparedStatement;


public class student implements ActionListener{

	JFrame studentFrame = new JFrame("student");
    static JButton studentAdd = new JButton("Add"); 
    static JTextField userNametext;
    static JTextField staffOrstudentText;
    static JTextField numberText;
    static JTextField addressText;
    static JTextField classText;
    static JTextField quantityText;
    
    student(){

        ImageIcon logo = new ImageIcon("src/logo.png");

        JLabel userNamelabel = new JLabel("Student name");
        userNametext = new JTextField();
        userNametext.setPreferredSize(new Dimension(250,40));
        
        JLabel staffOrstudentLabel = new JLabel("Student or Staff");
        staffOrstudentText = new JTextField();
        staffOrstudentText.setPreferredSize(new Dimension(250,40));

        JLabel numberLabel = new JLabel("Guardians contact number");
        numberText = new JTextField();
        numberText.setPreferredSize(new Dimension(250,40));

        JLabel addressLabel = new JLabel("Guardians address of residence");
        addressText = new JTextField();
        addressText.setPreferredSize(new Dimension(250,40));
        
        JLabel classLabel = new JLabel("Class");
        classText = new JTextField();
        classText.setPreferredSize(new Dimension(250,40));
        
        JLabel quantityLabel = new JLabel("Number of books allowed to borrow");
        quantityText = new JTextField();
        quantityText.setPreferredSize(new Dimension(250,40));

        studentAdd.setBounds(0, 900, 100, 20);
      
 
        
        
        studentFrame.setDefaultCloseOperation(JFrame.HIDE_ON_CLOSE);
        studentFrame.setSize(290, 500);
        studentFrame.setLayout(new FlowLayout());
        studentFrame.setVisible(true);
        studentFrame.setIconImage(logo.getImage()); 
        studentFrame.add(userNamelabel);
        studentFrame.add(userNametext);
        studentFrame.add(addressLabel);
        studentFrame.add(addressText);
        studentFrame.add(numberLabel);
        studentFrame.add(numberText);
        studentFrame.add(classLabel);
        studentFrame.add(classText);
        studentFrame.add(staffOrstudentLabel);
        studentFrame.add(staffOrstudentText);
        studentFrame.add(quantityLabel);
        studentFrame.add(quantityText);
        studentFrame.add(studentAdd);
        studentAdd.addActionListener(new Action());
        
    }
    
    static class Action implements ActionListener{

		public void actionPerformed(ActionEvent e) {
			
			try{
	             Class.forName("net.ucanaccess.jdbc.UcanaccessDriver");
	             Connection connection = DriverManager.getConnection("jdbc:ucanaccess://Database11.accdb");
	             System.out.println("Connected Successfully");
	             

				 String bookInsert =  "INSERT INTO UserInfoT (UserNaame, StaffOrStudent, ContactNumber, UserAddress, ClassOrDepartment, QuantityLimit) VALUES (?, ?, ?, ?, ?, ?)";
	             PreparedStatement pS = connection.prepareStatement(bookInsert);

	             pS.setString(1, userNametext.getText());
	             pS.setString(2, staffOrstudentText.getText());
	             pS.setString(3, numberText.getText());
	             pS.setString(4, addressText.getText());
	             pS.setString(5, classText.getText());
	             pS.setString(6, quantityText.getText());
           
	             int row= pS.executeUpdate();
	             
	             if (row > 0) {
	            	 System.out.println("A row has been inserted in books");
	             	}
	             
	             }
	             catch(Exception e1){
	          
	    	}
			
				}
		}

 
}
