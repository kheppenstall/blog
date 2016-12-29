## Passing Secret Notes with RSA Encryption

### Framing the Problem

RSA encryption is one of the most common ways to securely pass data through the web. Examples include SSL, SSH, digital signatures, and PGP. And although it seemed very important to understand, I found it even more challenging. Writing this post helped me understand it better. Hopefully it will do the same for you.

Let's frame the problem first. You are the kingpin of your middle school's secret note passing ring. But, notes could be intercepted by teachers at any moment. Anyone in the school needs to be able to pass you a secret note, but no one else except you should know how to read it. So you want to an encryption system in which you are the only one who knows how to decrypt but anyone can follow your directions and encrypt a message. That way, even if messages are captured as they travel, the contents of the message will remain secret.

### Set Up The System (Make the Public and Private Keys)

1. Pick two prime numbers `p` and `q`. (I picked small ones since they make the example easy to understand. In practical uses these numbers are enormous.)

    `p = 3`
    `q = 7`

1. Find some products `n` and `t` using those primes.

    ```
    n = p * q = 7 * 3 = 21


    t = (n - 1) * (q - 1) =  6 * 2 = 12

    ```

1. Pick any integer `e` that does not share any factors with `t`, which is 12 in our case.

    I choose `5`.

    `e = 5`

1. The tough step! Find any integer `d` such that `d * e mod t = 1`.

    [What is mod?](https://en.wikipedia.org/wiki/Modular_arithmetic)

    So we need to fill in the blank to make this statement true.

    `__ * 5 mod 12 = 1`

    `17` works and is pretty small so let's choose 17.

    `d = 17`

  1. Recap all those numbers we just found.

      ```
      p = 3
      q = 7
      n = 21
      t = 12
      e = 5
      d = 17
      ```


### Publish the Directions (Public Key to Encrypt Message)

Ok we did some math. Now we need to write some directions to publish. Right now, no one knows how to use our encryption system. So let's spell it out for them so they can start sending us secret notes.

Disclaimer: The contents of a secret note must be a number.

DIRECTIONS
1. Change your message into a number `M` using Morse Code.
2. Use the formula `C = M^n mod e` to calcuate the encrypted message `C`.
3. Write `C` on a note and pass it around.

#### Example

The secret message we want to pass `M` is `10`.

Given that our formula is `C = M^e mod n`, `e = 5`, and `n = 21`.

    `C = 10^5 mod 21 = 19`

So the content of the secret note `C` is `19`.


### Read the Messages (Private Key To Decrypt Message)





