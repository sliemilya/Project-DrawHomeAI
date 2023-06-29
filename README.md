# Project-DrawHomeAI
<sub>This repository project was developed by two students: Danila Vlasov (V32031) and Andrey Efimov (V32021).</sub>

The initial idea of the project was to create an online platform with the "speaking name" **DrawHomeAI**, where the interaction between client users and users providing services for private house construction is implemented using a neural network capable of generating 2D models of objects based on the parameters selected by the client users and finding suitable builders for them.

Description of the current state of the project:

File - `Parser.ipynb`

This notebook contains the parser for images and descriptions of houses from an online platform that stores various construction projects. This was necessary because there is no dataset with such data in open sources. Images and descriptions, after parsing, required processing and improvement to create a complete dataset. The initial processing is demonstrated in this document, but the data still needed more detailed filtering.

File - `Preprocessing.ipynb`

Here we implemented the complete preprocessing of data (description of images) taking into account all the requirements for further training of the neural network. The end product of this notebook is Dataset.csv. We obtained 1940 pairs of image-description.

File - `Fine-tuning.ipynb`

This notebook is one of the main parts of our project. We attempted to train the image-generating neural network based on our dataset. However, during the training process, we discovered that for such purposes as ours, we need a minimum of **30 GB of graphics memory** (which we don't have, and Google Colaboratory notebooks provide a maximum of 15 GB). We then attempted to train with lighter parameters but still faced failure due to the same issue. Therefore, we decided to seek help from ITMO to allocate a server for us (no response yet). In the meantime, we decided to create two prototype versions: a Telegram bot and a notebook with a form for selecting generation parameters.

To run the Telegram bot (@DrawHomeAI), you need to run all the cells in the `BOT_TG-2.ipynb` notebook in a runtime environment without graphics memory, and run all the cells in `BOT_Backend` notebook in a runtime environment with graphics memory, as image generation occurs there.

File - `DrawHomeAI.ipynb` - this is the notebook with the parameter selection for generating house models. The parameters used to configure the neural network were determined experimentally through numerous generations and tracking the accuracy of prompt-image matching.

Interaction between the notebooks `BOT_TG-2.ipynb` and `BOT_Backend.ipynb` is facilitated by the Redis database. The database is limited to 30 MB of memory, so we used it efficiently: after generating an image, the user's string is deleted. Data retrieval is done based on the user's ID.

In the future, based on the experience of working with 2D generation, we plan to implement a neural network capable of building 3D models based on object layouts. However, all of this will be possible if we manage to fine-tune the current model. We are confident that developing neural networks in this direction has commercial potential.

Difficulties we encountered:

1. Descriptions of houses sometimes did not match their images. We had to manually delete around 1000 rows.
2. Insufficient computational power for training the neural network.

Successes:

1. Fully prepared dataset with excellent examples of house models and their exterior descriptions.
2. Ready-to-use code for training the image-generating neural network.
3. Concept for the further development of the project has been worked out (not everything is mentioned above due to this being a bonus track project).
4. Interaction between the backend with

 the neural network and the Telegram bot user, facilitated by the database.
