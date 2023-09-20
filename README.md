**Image-in-Image Steganographer**

**Pitch**

Are you starting a stock image provider company and need a digital watermark? Do you have the need to send steamy photos to a lover behind your partner's back? Or are you simply a James Bond wannabe? Steganography has extensive use cases from digital rights management (DRM) to covert communication.

Our Image Steganographer will provide an intuitive platform that allows users to hide and extract images within a "cover" images, ensuring secure communication through obfuscation without visible alteration. Simply provide us with a "cover" image and a "payload" image, and we will hide the payload image into your cover image, with basically no visible alteration to your cover image. You can then easily pass off the resultant image as the original, with the hidden message that only your intended recipient will know exists. They can then recover the payload by re-submitting the composite image into our "retrieve" function, which will output the payload.

**Functionalities**

We will be creating an intuitive web application that will cater to the following functionalities:

1. Individualised user profile

1. Guest User: One time use and download. Input and output image is not stored in our database
2. Profiled User: Able to check encapsulation history and retrieve past embedded images.

1. Image Encryption

- User uploads a cover image and the payload image to be encapsulated.
- Website will output the encapsulated composite image.

1. Image Decryption:

- User uploads a composite image, and the program will decrypt it and output the cover and payload image.
- If the image is not a properly encrypted image, the program will also notify the user.

1. Image Download

- User can choose to download embedded image to disk.

1. Different levels of encoding

- Different image types require different encoding algorithms. We allow users to choose what kind of images they want to provide as the payload (BW, greyscale, RGB images).

**Major Components**

**Backend** :

We will be leveraging Django to handle all the program back end. We chose Django for its ease-of-use and rapid deployment capabilities and ease of integration with sql databases and frontend frameworks.

**Backend components:**

1. **Api Endpoints setup**

For APi endpoints setup, we will be using django rest framework (DRF) to set up the API end-points to communicate with the Vue.js frontend.

1. **Connection to MySql database**

Use the mysqlclient for python and configure the relevant database configurations.

1. **Main encryption unit**

Since we have to have different encryption schemas for different input payload types, we will create an Encryptor class as an abstract parent class.

We will then have different specific encryptor classes that inherit from the abstract Encryptor class. (e.g. ColorInColorEncryptor() or GreyScaleInColorEncryptor() ). They will individually define the necessary functions common to Encryptor objects. NOTE: Both encryption and decryption functionalities will be handled by the encryptor class.

Each view (a view is the function that handles web requests and sends web responses) will then call the relevant methods of the specific encryptor.

**Testing:**

The image encryption and decryption part of the program can be completely separately tested from the front-end or database components. We can just separately test it with python's built in unittest or pytest libraries.

- Step 1: Visual inspection of output image. Since our steganographer is used to trick the naked eye, a good litmus test is simply, "does the image still look the same?" for the encryption part and "did I recover a similar looking image" for the decryptor.
- Step 2: Do a pixel by pixel comparison with a testcase. More necessary when we are trying to use it to create digital watermarks.
- Step 3: Full-stack integration test - Test the upload/ download functionalities.

**Frontend** :

We will be using Vue.js to build the website frontend. We chose Vue.js for its shallow learning curve (we do not have much frontend experience), component based structure, and flexibility in terms of integration with backend services.

**Database** :

Data Storage is not a key feature of our application, but we are planning to create individual user profile functionalities, which will require user data to be stored in a database. We are picking a relational database as the data we are storing is simple and structured. This is also convenient because Django framework works by default, with a relational database. We will be using MySql for its lightweight, easy-to-use capabilities.

Database configurations will be done in settings.py as such:

| DATABASES = { 'default': { 'ENGINE': 'django.db.backends.mysql', 'NAME': 'your\_db\_name', 'USER': 'your\_mysql\_user', 'PASSWORD': 'your\_mysql\_password', 'HOST': 'localhost'} } |
| --- |

**Schedule**

**Week 1:**

Set up the project framework.

Build basic UI for uploading images.

**Week 2:**

Implement image embedding feature.

**Week 3:**

Implement image extraction feature.

Do tests for backend embed/ extract features.

**Week 4:**

Integrate backend with frontend

**Week 5 - Week 6:**

Build user profile features and integrate with database for CRUD operations..

**Week 7:**

Conduct rigorous combined component testing.

Start on presentation prep.

**Week 8:**

Finalize debugging of features and prepare for presentation.

**Continuous integration**

Utilise the Django testing framework through the means of integration testing

**Style Guide:**

We will be following the [Google Python Style Guide](https://github.com/google/styleguide/blob/gh-pages/pyguide.md) throughout our development.

An automated tool that can check whether our code matches this style guide is flake8.

To compute test coverage in Python, you can use a tool like coverage.py. This tool can monitor your Python programs and note which parts of the code have been executed.

**Risk**

1. **Image Quality Degradation** :

It is possible that using our current proposed method of encrypting the payload image into the cover image will result in significant quality degradation that is very obvious to the naked eye.

**Resolution** : Explore different embedding techniques, such as encrypting with a smaller payload image size, compression etc.

**Adjustment** : Allocate additional time for writing the encryption and decryption algorithms as well as testing.

2. **Integration errors between different components of the code**

There is a chance that there will be breakdown in REST GET/ POST request across the API endpoints between the frontend and backend.

**Resolution** : Do unit testing after each component we finish implementing to make sure it works before building more.

**Adjustment** : No adjustments to schedule required

**3. Large Image Sizes Causing Slow Processing:**

Slow processing speeds for large images may result in longer-than optimal wait times for the users.

**Resolution** : Optimise algorithms or provide guidelines on optimal image sizes.

**Adjustment** : To handle multiple requests at once, we may have to use python multiprocessing library.

**Teamwork and division of work**

We'll use Docker to create consistent development environments. Given that team members use different OS (Linux, Windows, Mac), Docker ensures consistent behaviour.

**Logan:** Work on testing / debugging of functionality.

**Jingbo:** Work on encryption/ decryption backend functionality.

**Yukang:** Work on designing front page

**Heng:** Work on database setup