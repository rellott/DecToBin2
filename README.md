# DecToBin2
 
#Main activity code:
 
    package com.example.dectobin2;

    import androidx.annotation.NonNull;
    import androidx.appcompat.app.AppCompatActivity;

    import android.os.Bundle;

    import com.google.android.gms.ads.AdListener;
    import com.google.android.gms.ads.AdRequest;
    import com.google.android.gms.ads.AdView;
    import com.google.android.gms.ads.LoadAdError;
    import com.google.android.gms.ads.MobileAds;

    import com.google.android.gms.ads.MobileAds;
    import com.google.android.gms.ads.initialization.InitializationStatus;
    import com.google.android.gms.ads.initialization.OnInitializationCompleteListener;


    import android.view.View;
    import android.view.View.OnClickListener;
    import android.widget.Button;
    import android.widget.EditText;
    import android.widget.RadioButton;
    import android.widget.Toast;

    public class MainActivity extends AppCompatActivity implements OnClickListener{

    private Button Convert;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        AdView mAdView = findViewById(R.id.adView);
        AdRequest adRequest = new AdRequest.Builder().build();
        mAdView.loadAd(adRequest);

        mAdView.setAdListener(new AdListener() {
            @Override
            public void onAdLoaded() {
                // Code to be executed when an ad finishes loading.
            }

            @Override
            public void onAdFailedToLoad(@NonNull LoadAdError adError) {
                // Code to be executed when an ad request fails.
            }

            @Override
            public void onAdOpened() {
                // Code to be executed when an ad opens an overlay that
                // covers the screen.
            }

            @Override
            public void onAdClicked() {
                // Code to be executed when the user clicks on an ad.
            }

            @Override
            public void onAdClosed() {
                // Code to be executed when the user is about to return
                // to the app after tapping on an ad.
            }
        });


        Convert = (Button) findViewById(R.id.Convert);
        Convert.setOnClickListener((OnClickListener) this);
    }

    @Override
    public void onClick(View v)
    {
        RadioButton radio_dec_from, radio_bin_from, radio_dec_to, radio_bin_to;

        radio_dec_from = (RadioButton) findViewById(R.id.radio_dec_from);
        radio_bin_from = (RadioButton) findViewById(R.id.radio_bin_from);
        radio_dec_to = (RadioButton) findViewById(R.id.radio_dec_to);
        radio_bin_to = (RadioButton) findViewById(R.id.radio_bin_to);

        if (radio_dec_from.isChecked()){
            if (radio_bin_to.isChecked()){
                if(Convert.equals(v))
                {
                    int dec = -1;

                    EditText decText = (EditText) findViewById(R.id.Number);
                    String decStr = decText.getText().toString();

                    if(decStr.length() > 0 && decStr.length() < 9)
                    {
                        dec = Integer.parseInt(decStr);
                    }
                    else{
                        Toast toast = Toast.makeText(getApplicationContext(),
                                "Неверный диапазон значений", Toast.LENGTH_SHORT);
                        toast.show();
                    }

                    if(dec >= 0)
                    {
                        String bin = "";
                        while(dec != 0)
                        {
                            if(dec % 2 == 0)
                            {
                                bin = "0" + bin;
                            }
                            else
                            {
                                bin = "1" + bin;
                            }
                            dec = dec / 2;

                            EditText binText = (EditText) findViewById(R.id.Result);
                            binText.setText(bin);
                        }
                    }
                }
            }
            else{
                EditText decText = (EditText) findViewById(R.id.Number);
                String decStr = decText.getText().toString();

                EditText binText = (EditText) findViewById(R.id.Result);
                binText.setText(decStr);
            }
        }
        else{
            String regex = "[0-1]*";
            EditText decText = (EditText) findViewById(R.id.Number);
            String decStrtest = decText.getText().toString();
            if (!decStrtest.matches(regex)){
                Toast toast = Toast.makeText(getApplicationContext(),
                        "Число должно быть двоичным", Toast.LENGTH_SHORT);
                toast.show();
            }
            else{
                if(radio_dec_to.isChecked()){
                    String decStr = decText.getText().toString();

                    int decimalValue = Integer.parseInt(decStr, 2);

                    EditText binText = (EditText) findViewById(R.id.Result);
                    binText.setText(String.valueOf(decimalValue));
                }
                else{
                    String decStr = decText.getText().toString();

                    EditText binText = (EditText) findViewById(R.id.Result);
                    binText.setText(decStr);
                }
            }

        }


    }

    }

