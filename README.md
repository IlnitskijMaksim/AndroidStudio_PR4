# Практична робота №4
### Тема роботи:
Робота із кольором та локалізацією в ОС Android.
### Мета роботи:
Отримати досвід роботи із використанням значень
рядків і кольорів та зміною локалізації у додатку.
# Хід роботи

### Зміна кольорів та локалізація

```java
package com.example.pr1;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.content.ContextCompat;

import android.graphics.Color;
import android.graphics.drawable.GradientDrawable;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import android.widget.LinearLayout;

import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    private Button simpleButton;
    private TextView simpleTextView;
    private int i = 0;

    private boolean isUkrainianLocale() {
        Locale currentLocale = getResources().getConfiguration().locale;
        String currentLanguage = currentLocale.getLanguage();
        return currentLanguage.equals("uk");
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        simpleButton = findViewById(R.id.simpleButton);
        simpleTextView = findViewById(R.id.simpleTextView);

        LinearLayout linearLayout = findViewById(R.id.linearLayout);

        int blue = ContextCompat.getColor(this, R.color.blue_ua);
        int yellow = ContextCompat.getColor(this, R.color.yellow_ua);
        int black = ContextCompat.getColor(this, R.color.black);
        int red = ContextCompat.getColor(this, R.color.red );

        GradientDrawable gradientDrawableUA = new GradientDrawable(GradientDrawable.Orientation.TOP_BOTTOM,
                new int[]{blue, yellow});

        GradientDrawable gradientDrawableAnother = new GradientDrawable(GradientDrawable.Orientation.TOP_BOTTOM,
                new int[]{black, red});

        if (isUkrainianLocale()){
            linearLayout.setBackground(gradientDrawableUA);
            simpleButton.setText(R.string.button_ua);
        }
        else {
            linearLayout.setBackground(gradientDrawableAnother);
            simpleButton.setText(R.string.button_en);
            simpleTextView.setTextColor(Color.WHITE);
        }

        simpleButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (isUkrainianLocale()) {
                    if (i == 0) {
                        simpleTextView.setText(R.string.hello_ua);
                        i++;
                    } else if (i == 1) {
                        simpleTextView.setText(R.string.stop_ua);
                        i++;
                    } else {
                        simpleTextView.setText(R.string.emoji_ua);
                        i = 0;
                    }
                } else {
                    linearLayout.setBackground(gradientDrawableAnother);
                    if (i == 0) {
                        simpleTextView.setText(R.string.hello_en);
                        i++;
                    } else if (i == 1) {
                        simpleTextView.setText(R.string.stop_en);
                        i++;
                    } else {
                        simpleTextView.setText(R.string.emoji_en);
                        i = 0;
                    }
                }
            }
        });
    }

    @Override
    protected void onStart() {
        super.onStart();
        showScreenMessage("App started", Toast.LENGTH_SHORT);
    }

    @Override
    protected void onRestart() {
        super.onRestart();
        showScreenMessage("App restarted", Toast.LENGTH_SHORT);
    }

    @Override
    protected void onPause() {
        super.onPause();
        showScreenMessage("App paused", Toast.LENGTH_SHORT);
    }

    private void showScreenMessage(String message, int duration) {
        Toast.makeText(this, message, duration).show();
    }
}
```

### Як працює програма

Якщо на пристрої стоїть українська мова, то відображається так:

https://github.com/IlnitskijMaksim/AndroidStudio_PR4/assets/112692170/88047a6b-0ea9-449c-a9c0-36e0b82f0b30

Якщо на пристрої стоїть інша мова, то виводиться англійська мова тексту та тексту на кнопці та інші кольори:

![Screenshot_3](https://github.com/IlnitskijMaksim/AndroidStudio_PR4/assets/112692170/cc345db1-d0c6-4cbe-b4c0-05cbf924edc5)

![Screenshot_11](https://github.com/IlnitskijMaksim/AndroidStudio_PR4/assets/112692170/c04b8fba-f3bf-4389-9d37-56d8e452309b)



