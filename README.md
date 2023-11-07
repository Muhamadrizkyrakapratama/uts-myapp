# UTS-Pemograman_Mobile
```
Nama  : Muhamad rizky raka pratama
Nim   : 312210397
Kelas : TI.22.A4
Dosen : Donny Maulana, S.Kom., M.M.S.I.
```

**Tugas Uts** ```Soalnya adalah dari project sebelumnya Toast number dan Buatlah Method Program java Toast Number, dengan menghasilkan Bilangan Fibonacci```

# Deret Fibonacci

## Definisi Deret Fibonacci

>**Deret Fibonacci** adalah urutan angka yang dimulai dengan angka 0 dan 1, kemudian setiap angka berikutnya adalah hasil penjumlahan dari dua angka sebelumnya. Dengan demikian, deret ini memiliki pola pertumbuhan eksponensial. **Deret Fibonacci** biasanya ditulis sebagai berikut :
>
>``0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...``
>
>Dalam deret ini, angka pertama adalah 0, angka kedua adalah 1, dan setelah itu, setiap angka berikutnya adalah hasil penjumlahan dari dua angka sebelumnya. Misalnya, 2 adalah hasil penjumlahan dari 1 + 1, 3 adalah hasil penjumlahan dari 1 + 2, 5 adalah hasil penjumlahan dari 2 + 3, dan seterusnya.
>
>**Deret Fibonacci** pertama kali diperkenalkan oleh matematikawan Italia bernama ``Leonardo of Pisa``, yang juga dikenal sebagai Fibonacci, dalam bukunya "Liber Abaci" pada tahun 1202. Deret ini muncul dalam berbagai konteks dalam matematika, ilmu komputer, ilmu alam, dan banyak bidang lainnya. Beberapa aplikasi dari deret Fibonacci meliputi permodelan pertumbuhan populasi, analisis pasar keuangan, dan desain algoritma.

## **Program Fibonacci**
### **Main Activity Java**
```java
package com.example.fibonacciapp;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.content.ContextCompat;

import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private long fibMinus1 = 0;
    private long fibMinus2 = 1;
    private long currentFib = 0;
    private TextView mShowFibonacci;
    private long i = 0;

    private long n = 0;
    private long limit = 0; // Menyimpan batas Fibonacci yang diinginkan

    private EditText mLimitInput;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mShowFibonacci = (TextView) findViewById(R.id.show_count);
        mLimitInput = (EditText) findViewById(R.id.limit_input);
        updateFibonacciDisplay();
    }

    public void countUp(View view) {
        if (mLimitInput.getText().toString().isEmpty()) {
            Toast.makeText(this, "Enter the limit first", Toast.LENGTH_SHORT).show();
            return;
        }

        limit = Long.parseLong(mLimitInput.getText().toString());

        if (n >= limit) {
            Toast.makeText(this, "Fibonacci limit reached", Toast.LENGTH_SHORT).show();
            return; // Hentikan perhitungan jika jumlah baris Fibonacci mencapai batas
        }

        long newFib = fibMinus1 + fibMinus2;
        fibMinus2 = fibMinus1;
        fibMinus1 = newFib;
        currentFib = newFib;
        n++; // Inkrementasi jumlah baris Fibonacci

        updateFibonacciDisplay();
    }



    public void showFibonacci(View view) {
        Toast toast = Toast.makeText(this, R.string.fibonacci_message, Toast.LENGTH_SHORT);
        toast.show();
    }

    public void reset(View view) {
        currentFib = 0;
        fibMinus2 = 1;
        fibMinus1 = 0;
        limit = 0;
        n = 0;
        mLimitInput.setText(""); // Mengosongkan input
        updateFibonacciDisplay();
    }

    private void updateFibonacciDisplay() {
        if (mShowFibonacci != null) {
            mShowFibonacci.setText(Long.toString(currentFib));
            mShowFibonacci.setTextColor(getFibonacciColor());
        }
    }

    private int getFibonacciColor() {
        // Gantilah warna berdasarkan nilai Fibonacci
        i++;
        if (i % 2 == 0) {
            return ContextCompat.getColor(this, R.color.colorFibonacciBlue);
        } else {
            return ContextCompat.getColor(this, R.color.colorFibonacciGreen);
        }
    }
}
```

### **String.xml**
```xml
<resources>
    <string name="app_name">FIbonacciApp</string>
    <string name="button_label_count">Count</string>
    <string name="button_label_fibonacci">Fibonacci</string>
    <string name="fibonacci_message">Program Fibonacci</string>
</resources>
```

### **Colors.xml**
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="blue">#0000FF</color>
    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
    <color name="colorNumber">#69BE28</color>
    <color name="colorFibonacciBlue">#0000FF</color> 
    <color name="colorFibonacciGreen">#008000</color> 
</resources>
```

### **activity_main.xml**
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.fibonacciapp.MainActivity">
    <Button
        android:id="@+id/button_fibonacci"
        android:layout_width="150dp"
        android:layout_height="50dp"
        android:layout_marginEnd="8dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:background="@color/colorPrimary"
        android:onClick="showFibonacci"
        android:text="@string/button_label_fibonacci"
        android:textColor="@android:color/white"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="OnClick"/>

    <EditText
        android:id="@+id/limit_input"
        android:layout_width="160dp"
        android:layout_height="50dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:background="@color/colorPrimary"
        android:textAlignment="center"
        android:textColor="@color/white"
        android:hint="Enter limit"
        android:textColorHint="@color/white"
        android:inputType="number"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/button_count"
        android:layout_width="160dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="4dp"
        android:background="@color/colorPrimary"
        android:onClick="countUp"
        android:text="@string/button_label_count"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"/>

    <Button
        android:id="@+id/button_reset"
        android:layout_width="160dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="4dp"
        android:background="@color/colorPrimary"
        android:onClick="reset"
        android:text="Reset"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        tools:ignore="OnClick"/>

    <TextView
        android:id="@+id/show_count"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        android:background="#FFFF00"
        android:gravity="center_vertical"
        android:text="0"
        android:textAlignment="center"
        android:textColor="@color/colorPrimary"
        android:textSize="160sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@+id/button_count"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/button_fibonacci"
        app:layout_constraintVertical_bias="0.0"
        tools:ignore="RtlCompat"/>
</androidx.constraintlayout.widget.ConstraintLayout>
```

## Output  

- Berikut adalah tampilan apabila ``telah berhasil di RUN`` di awali dengan angka 0.  

![Screenshot (46)](https://github.com/HasbiAssidiki/UTS-Pemograman_Mobile/assets/115614317/5753c2e7-f08e-4348-bb71-a49c52607a12)  

## Output  

- Selanjutnya, sebelum ``mengklik tombol Count``, sebaiknya isi angka pada Enter Limit terlebih dahulu. Sebagai contoh, saya mengisi limit dengan angka 10.  

![Screenshot (47)](https://github.com/HasbiAssidiki/UTS-Pemograman_Mobile/assets/115614317/6a6eea25-fb16-4dba-9443-4633fb7b9a6c)  


## Output 

- Selanjutnya, bisa langsung ``klik tombol Count``. Maka, tampilannya akan berubah dari angka 0 menjadi angka 1.  

![Screenshot (48)](https://github.com/HasbiAssidiki/UTS-Pemograman_Mobile/assets/115614317/bc796f4a-41a8-48da-94f6-7fcdc10221e4)  

## Output

- **Deret Fibonacci** memiliki pola sebagai berikut: ``0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...`` Oleh karena itu, setelah angka 1 muncul, angka berikutnya juga akan menjadi angka 1. Perubahan angka ini ditandai dengan perubahan warna pada angka tersebut.  

![Screenshot (49)](https://github.com/HasbiAssidiki/UTS-Pemograman_Mobile/assets/115614317/551f8b4b-773b-43fc-9062-c1c8f7e1d087)  


## Output

- Selanjutnya, setelah angka 1 muncul dua kali, angka berikutnya akan menjadi 2. Angka-angka selanjutnya akan mengikuti urutan deret Fibonacci, yaitu ``0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ....``  

![Screenshot (50)](https://github.com/HasbiAssidiki/UTS-Pemograman_Mobile/assets/115614317/ca241bd4-4872-424a-9863-6e5e56d0cbd3)  


## Output

- Ketika deret Fibonacci mencapai limit, maka akan tampil teks *"Fibonacci limit reached"*. Ketika kita ``klik tombol Count``, maka tidak akan dilanjutkan dan hanya berhenti di angka limit tersebut.  

![Screenshot (51)](https://github.com/HasbiAssidiki/UTS-Pemograman_Mobile/assets/115614317/ab4f51e2-9233-4570-b7a2-fb0d07f9d015)  

## Output

- Selanjutnya, jika kita ``klik tombol Fibonacci,`` maka akan muncul tampilan teks *"Program Fibonacci"*.  

![Screenshot (52)](https://github.com/HasbiAssidiki/UTS-Pemograman_Mobile/assets/115614317/ae803dc0-8dbf-43aa-8f08-3191378c9b3a)  

## Ouput

- Terakhir, ini adalah tampilan apabila ``diklik tombol Reset``, semua akan kembali ke tampilan awal, dimulai dari angka 0, dan harus memasukkan limit lagi.  

![Screenshot (53)](https://github.com/HasbiAssidiki/UTS-Pemograman_Mobile/assets/115614317/298309e0-9d35-4a30-90fc-5d72d44bdb9c)  

## SELESAI !!