# imessage-rnn

In-progress project: Building a neural network to learn an individual's style of speaking, and respond in their manner.

**Current State:**
Trained on my iMessages from the past year (many of which are with my mom). **60%** accuracy in letter-by-letter message generation. Disclaimer: I am not responsible for what the neural network generates!
[RNN Live Chat - Web version](http://imessage-chatbot.anastassia.io/)

### Technologies

* Training messages obtained with **SQL**
* Recurrent Neural Network (RNN) built with **TensorFlow**
* **Flask** app responds with generated messages to a **Twilio SMS** webhook
* **AWS EC2**: Trained RNN on p2.xlarge instance, message generator deployed through t2.micro instance

### Implementation


#### 1. Extract Data

Data was extracted from the iMessage sqlite3 database, located in `/Library/Messages/chat.db`.

Getting all messages from yourself:
```sql
SELECT text FROM message WHERE is_from_me = 1;
```

Getting all messages from another person:
```sql
-- get their handle_id
SELECT * FROM handle WHERE id="(their_phone_number)";
-- use it to extract their messages
SELECT text FROM message WHERE handle_id = "(handle_id)" AND is_from_me = 0;
```

Save the ascii messages to a .txt file and format it (ie; deal with emojis).

#### 2. Process Data

With `dataset.py`, process the text data with parameters from `config.py` into _batches_. The input shape for the recurrent neural network is: (None, 32, 62, 256).

#### 3. Train the Recurrent Neural Network model

Now draw the rest of the owl

#### 4. Use the model to generate text


### Next Steps

- [x] Improve RNN performance with LSTM cells
- [x] In progress: Increase training data
- [x] In progress: Build web app version with **React**
- [ ] Generate responses of varying lengths
- [ ] Look into Natural Language Processing (NLP)
