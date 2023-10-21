# Lab Report 2
## String Server Code
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.

    int count = 0;
    String output = "";
    
    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "Use /add-message?s=word to add words. Replace 'word' with the word you want to add.";
        } else if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if(parameters[0].equals("s")) {
                String word = parameters[1].replace('+', ' ');
                count++;
                output += count + ". " + word + "\n";
                return output;
            }
            return "Invalid command.";
        } else {
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
## Screenshots of /add-message
![Screenshot 1](https://imgur.com/0cbAqrf) <br>
![Screenshot 2](https://imgur.com/JR8LKJO)
