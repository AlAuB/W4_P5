# W4_P5
 Part5 for Worksheet4 (Hangman Game)



## The detailed info about this APP

This app has two parts: one `MainActivity` and one `Fragment`.

The `Fragment ` is kind of *“lightweight”* activity that can be embed in their parent activity.

The `MainActivity` controls the A-Z, restart game, and hint buttons.

The `Fragment` has ImageView, and TextView.

`MainActivity` call public functions to interact with `Fragment`. However, it is much harder to let `Fragment` sends info back to `MainActivity`.



### How to let `MainActivity` and `Fragment` communicate with each other:

**One way to do this:**

1. Create an **interface** and create methods for that interface (This allow you make your own version Listener).

   ```java
   public interface gameListener {
   		void getResult(String input);
   }
   ```

2. Initialize a new variable for the interface, and call the method when you want to pass info to `MainActivity`.

   ```java
   private gameListener listener;
   
   listener.getResult("finish"); //Pass String "finish" to MainActivity
   ```

3. Attach your own listener to the environment (Activity) by override `onAttach()` function.

   ```java
   @Override
   public void onAttach(@NonNull Context context) {
   		super.onAttach(context);
       if (context instanceof gameListener)
         	listener = (gameListener) context;
   }
   ```

4. Implement this interface in `MainActivity` so it can get info from `Fragment`.

   ```java
   public class MainActivity extends AppCompatActivity implements Game.gameListener{
     	Game game = New Game();
     
     	@Override
       public void getResult(String input) {
           if (input.equals("finish")) {
               // Do something
           }
       }
   }
   ```

   
