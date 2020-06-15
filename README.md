java file 
// Add your package below
package com.example.android.justjava;

import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import android.view.View;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.TextView;
import java.text.NumberFormat;
/**
 * This app displays an order form to order coffee.
 */

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    int quantity=0;
    /**
     * This method is called when the order button is clicked.
     */
    public void submitOrder(View view) {
        CheckBox whippedCream = (CheckBox) findViewById(R.id.whipped_cream_checkbox);
        boolean haswhippedCream =whippedCream.isChecked();
        CheckBox chocolate = (CheckBox) findViewById(R.id.chocolate_checkbox);
        boolean haschocolate =chocolate.isChecked();
        EditText nameFeild = (EditText) findViewById(R.id.name_edit_view);
        String name = nameFeild.getText().toString();
        int price = calculateprice(haschocolate , haswhippedCream);
        String priceMessage =createOrderSummary(price , haswhippedCream , haschocolate , name);
        displaymessage(priceMessage);
    }
    /**
     * This method increment the quantity value on the screen.
     */
    public void increment(View  view) {
        display(++quantity);
        displayPrice(quantity*5);
    }

    /**
     * This method calculate final prce value on the screen.
     */
    public int calculateprice( boolean addchocolate , boolean addwhippedcream ){
        if (addchocolate && addwhippedcream){
            return quantity*8;
        } else if (addchocolate){
            return quantity*7;
        } else if (addwhippedcream){
            return quantity*6;
        } else{
            return quantity*5;
        }
    }
    /**
     * This method decrement the quantity value on the screen.
     */
    public void decrement(View view) {
        if (quantity > 0) {
            display(--quantity);
            displayPrice(quantity * 5);
        } 
    }

    /**
     * This method displays the given quantity value on the screen.
     */
    private void display(int number) {
        TextView quantityTextView = (TextView) findViewById(R.id.quantity_text_view);
        quantityTextView.setText("" + number);
    }
    /** this craeate order summery
     */
    private String createOrderSummary(int price , boolean addwhippedcream , boolean addchocolate , String addname){
        String priceMessage ="Name : " + addname;
        priceMessage += "\nAdd whipped creame :" + addwhippedcream;
        priceMessage += "\nAdd chocolate :" + addchocolate;
        priceMessage += "\nQuantity " + quantity;
        priceMessage += "\nTotal : $" + price ;
        priceMessage += "\nThank You!";
        return priceMessage;
    }

    /**
     * This method displays the given price on the screen.
     */
    private void displayPrice(int number) {
        TextView priceTextView = (TextView) findViewById(R.id.price_text_view);
        priceTextView.setText(NumberFormat.getCurrencyInstance().format(number));

    }
    /**
     * This method displays the given message on the screen.
     */
    private void displaymessage(String number) {
        TextView priceTextView = (TextView) findViewById(R.id.price_text_view);
        priceTextView.setText(number);

    }
}

xml file    

<?xml version="1.0" encoding="utf-8"?>
<ScrollView
    android:layout_height="match_parent"
    android:layout_width="match_parent"
    xmlns:android="http://schemas.android.com/apk/res/android">
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:conatext=".MainActivity">

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/name_edit_view"
        android:hint="Name"
        android:inputType="textCapWords" />

    <TextView
        android:layout_marginTop="16dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="toppigs"
        android:textAllCaps="true"
        android:layout_marginLeft="16sp"
        android:paddingBottom="16dp"
        />

    <CheckBox
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Whipped cream"
        android:textSize="16sp"
        android:paddingLeft="24dp"
        android:id="@+id/whipped_cream_checkbox"/>

    <CheckBox
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="chocolate"
        android:textSize="16sp"
        android:paddingLeft="24dp"
        android:id="@+id/chocolate_checkbox"/>

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Quantity"
        android:paddingTop="16dp"
        android:textAllCaps="true"
        android:layout_marginLeft="16sp"
            />

    <LinearLayout
         android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:layout_width="48dp"
            android:layout_height="48dp"
            android:layout_marginTop="16sp"
            android:layout_marginLeft="16sp"
            android:text="-"
            android:onClick="decrement"/>

        <TextView
            android:id="@+id/quantity_text_view"
            android:layout_width="wrap_content"
            android:layout_gravity="center"
            android:layout_height="wrap_content"
            android:layout_marginLeft="16sp"
            android:text="0"
            android:textColor="@android:color/black"
            android:textSize="16sp" />

        <Button
            android:layout_width="48dp"
            android:layout_height="48dp"
            android:layout_marginTop="16sp"
            android:layout_marginLeft="16sp"
            android:text="+"
            android:onClick="increment"
            android:layout_marginBottom="16sp"/>

    </LinearLayout>
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="order summary"
        android:layout_marginLeft="16sp"
        android:textAllCaps="true"
        android:layout_marginBottom="16sp"
        android:layout_marginTop="16sp"/>

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="$0"
        android:layout_marginLeft="16sp"
        android:textSize="16sp"
        android:textColor="@android:color/black"
        android:id="@+id/price_text_view"
        />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16sp"
        android:layout_marginLeft="16sp"
        android:text="order"
        android:onClick="submitOrder"/>


</LinearLayout>
</ScrollView>
