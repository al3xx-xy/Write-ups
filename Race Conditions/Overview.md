## Real World Analogy

Picture the following situation. You call a restaurant to reserve a table for a crucial business lunch. You are familiar with the restaurant and its setup. One particular table, number 17, is your preferred choice, considering it has a nice view and is relatively isolated. You call to make a reservation for Table 17; the host confirms it is free as no “Reserved” tag is placed on it. At the same time, another customer is talking with another host and making a reservation for the same table.

A *race condition* happens when *two or more things (like programs or threads)* try to *use or change the same data at the same time*, and the *result depends on who gets there first* — like a race.

Race conditions are a common type of vulnerability closely related to business logic flaws. They occur when websites process requests concurrently without adequate safeguards. This can lead to multiple distinct threads interacting with the same data at the same time, resulting in a "collision" that causes unintended behavior in the application. A race condition attack uses carefully timed requests to cause intentional collisions and exploit this unintended behavior for malicious purposes.

Let’s say we are tasked with testing the security of an online shopping web application. Many questions pop up. Can we reuse a single $10 gift card to pay for a $100 item? Can we apply the same discount to our shopping cart multiple times? The answer is _maybe_! If the system is susceptible to a race condition vulnerability, we can do all this and more.

