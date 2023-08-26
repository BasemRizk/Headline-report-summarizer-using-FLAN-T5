#  Headline report summarizer FLAN-T5 <br/>

##### Data Source: https://www.kaggle.com/datasets/sunnysai12345/news-summary<br/>

##### How it work ?<br/>

- Download the dataset from the link above.<br/>
- Install and import Dependencies needed for the project.<br/>
- Read trhe csv file as dataframe.<br/>
- Convert the text column to list and the headline column to another list.<br/>
- Split our data to training and testing.<br/>
- Convert Dataframe to DatasetDict which is more efficient for loading and processing data.<br/>
- It stores the data in a more compact format, which can save memory and speed up the training process.<br/>
- Use the google/flan-t5-base model and tokenizer.<br/>
- Check the maximun length for a sequence in text and headline to be used in padding as max_length parameter.<br/>
- preprocess_text function helps in encoding ,tokenizing and padding both texts and labels and set the padded token to -100 to be ignored.<br/>
- map the function on the dataset dict to be applied on each text and headline.<br/>
- We will use the rouge metric to evaluate our model which is better in evaluating (text summarization).<br/>
- postprocess_text function that is used for extracting words from the test headline and the predicted headlines from the test texts.<br/>
- In compute_metrics function we decode the tokenized text and headlines except the special tokens , then we use the postprocess_text to compare the results from the predicted and actual words and compute the rouge score from it.<br/>
- Use Data collator and pass the model,tokenizer,label_pad_token_id and pad_of_multiple_of which can make the data more consistent and easier to work with. When the sequences in a batch are all the same length, it makes it easier to apply certain operations to the data, such as batch normalization.<br/>
- Set the training argumetns for the trainer ,I set per_device_train_batch_size=8 depends on my GPU Cores and fp16=False (to avoid additional computational cost) This means that the model will be trained using 32-bit floating point precision.<br/>
- Also we set predict_with_generate=True, to generate text during evaluation which increase the accuracy of the model but it also make it more slower.<br/>
- We set save_total_limit = 2 which is the best and last one ,save_strategy="no" to save memory from saving each checkpoint.<br/>
- Create a training instance using model,data collator ,training and testing data and computing metrics.<br/>
-train the trainer and evaluate it(It may take long time depends on the amount of data and number of epochs).<br/>
- If we see the evaluation of the model it scores a good rouge score.<br/>
- Save the model and tokenizer to be reused again later.<br/>
- Load the model and use the pipeline to use while inference.<br/>
- Select a random sample text and use the pipeline to generate a headline text for it.
