# TIC-TAC-TOE
Get the code of layout of a basic app and logic of the game.
//***** TIC TAC TOE*****

//activity_main.xml  (Code for layout of the app)

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_marginTop="23dp"
    android:contentDescription="@string/grid"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="23sp"
        android:text="@string/Heading"
        android:textSize="36sp"
        android:textStyle="bold|italic"
        app:fontFamily="cursive"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <ImageView
        android:id="@+id/imageView122"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:contentDescription="@string/grid"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView"
        app:srcCompat="@drawable/grid" />

    <LinearLayout
        android:id="@+id/linearLayout"
        android:layout_width="0dp"
        android:layout_height="420dp"
        android:orientation="vertical"
        app:layout_constraintBottom_toBottomOf="@+id/imageView122"
        app:layout_constraintEnd_toEndOf="@+id/imageView122"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/imageView122">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/imageView0"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="0" />

            <ImageView
                android:id="@+id/imageView1"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="1" />

            <ImageView
                android:id="@+id/imageView2"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="2" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/imageView3"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="3" />

            <ImageView
                android:id="@+id/imageView4"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="4" />

            <ImageView
                android:id="@+id/imageView5"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="5" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/imageView6"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="6" />

            <ImageView
                android:id="@+id/imageView7"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="7" />

            <ImageView
                android:id="@+id/imageView8"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="playerTap"
                android:padding="20sp"
                android:tag="8" />
        </LinearLayout>

    </LinearLayout>

    <TextView
        android:id="@+id/status"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="15sp"
        android:layout_marginBottom="15sp"
        android:text="X's Turn- Tap to play"
        android:textSize="18sp"
        android:textStyle="italic"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/linearLayout"
        app:layout_constraintVertical_bias="0.984" />

</androidx.constraintlayout.widget.ConstraintLayout>



//MainActivity.java    (Code for Game)


package com.example.tiktactoe;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.ImageView;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    boolean gameActive = true;
    //  Player representation
    // 0-X
    // 1-O
    int activePlayer =0;
    int[] gameState ={2, 2, 2, 2, 2, 2, 2, 2, 2};
    //  State meanings:
    //  0-X
    //  1-O
    //  2-Null
    int [][] winPositions ={{0,1,2}, {3,4,5}, {6,7,8},
                            {0,3,6}, {1,4,7}, {2,5,8},
                            {0,4,8}, {2,4,6}};
    public void playerTap(View view) {
        ImageView img = (ImageView) view;
        int tappedImage = Integer.parseInt(img.getTag().toString());
        if(!gameActive){
            gameReset(view);
        }
        if (gameState[tappedImage] == 2 && gameActive) {
            gameState[tappedImage] = activePlayer;
            img.setTranslationY(-1000f);
            if (activePlayer == 0) {
                img.setImageResource(R.drawable.x);
                activePlayer = 1;
                TextView status = findViewById(R.id.status);
                status.setText("O's Turn- Tap to play");
            } else {
                img.setImageResource(R.drawable.o);
                activePlayer = 0;
                TextView status = findViewById(R.id.status);
                status.setText("X's Turn- Tap to play");
            }
            img.animate().translationYBy(1000f).setDuration(300);
        }
        // Check if any player has won
        for(int[] winPosition: winPositions){
           if( gameState[winPosition[0]] == gameState[winPosition[1]] &&
                   gameState[winPosition[1]] == gameState[winPosition[2]]&&
                   gameState[winPosition[0]] !=2){
               // Somebody has won! - Find out who!
               String winnerStr;
               gameActive = false;
               if(gameState[winPosition[0]] == 0){
                   winnerStr = "X has won";
               }
               else {
                   winnerStr = "O has won";
               }
               // Update the status bar for winner announcement
               TextView status = findViewById(R.id.status);
               status.setText(winnerStr);
           }
        }
    }
    public void gameReset(View view) {
        gameActive = true;
        activePlayer = 0;
        for(int i=0; i<gameState.length;i++){
            gameState[i] = 2;
        }
        ((ImageView)findViewById(R.id.imageView0)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView1)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView2)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView3)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView4)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView5)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView6)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView7)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView8)).setImageResource(0);

        TextView status = findViewById(R.id.status);
        status.setText("X's Turn- Tap to play");
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}



