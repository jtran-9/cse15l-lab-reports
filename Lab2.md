# Lab Report 2

## Part 1

### String Server Code
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
### Screenshots of /add-message
![Screenshot 1](https://i.imgur.com/eqXGaIm.png)
The handleRequest method got called when I used /add-message. The only argument for this method would be the url of the server that's sent to the StringServer. The relevant fields in the class would probably be the "count", "output", and "word" variables. <br> <br>
When /add-message was first sent, the "count" was incremented from 0 to 1. This variable is made for the numbering of the words in the list. Since this is the first word, we incremenet the value of "count" to 1. "word" is set to the string sent in through the query, which in this case was "Hello". This variable stores the current word or sentence that was sent by the user for future use. Finally, "output" was originally an empty string, "", but after this call, we concatenate the empty string with ' count + ". " + word + "\n" ', this helps create the list-like format that the user sees in the web browser. We then return "output" which prints "1. Hello" to the web browser for the user to see.
<br> <br>
![Screenshot 2](https://i.imgur.com/JR8LKJO.png)
For this call, the methods and relevant fields are the same as previously stated with the addition of the .replace() method. The handleRequest gets called when the user uses /add-message for the second time. The argument is once again just the url of the server. The relevant fields are still "count", "word", and "output". <br> <br>
When /add-message is called for the second time with the string input, "How are you", as the query, the "count" gets incremented again from 1 to 2, indicating that this is the second word that is going to be added. For "word", this time instead of 1 word, the string entered was a sentence with spaces. This means that the string that's sent to "word" originally is just "How+are+you". To get rid of those "+"s we call the .replace('+', ' ') method to replace all "+"s with spaces, to make it look exactly like what the user had typed in. The "output" is similar to the first case but this time, instead of holding an empty string, it currently holds "1. Hello\n". The "\n" indicates that there should be a new line, so when we add "2. How are you\n", it will be printed on a new line. The result of returning "output" is shown in the screenshot above.

## Part 2

### Path to Private Key 
![Path to Private Key](https://i.imgur.com/vYa0CbL.png)

### Path to Public Key
![Path to Public Key](https://i.imgur.com/KNGXOyd.png)

### Logging In Without Typing Password
![No Password Needed](https://i.imgur.com/Dkw8LvE.png)

## Part 3
One thing that stood out to me was learning about scp and mkdir as I had never really heard of those commands before working with them in lab this week. Their command abbreviations weren't as easy to decipher compared to commands like 'ls' and 'cat'.
