# HealingSpace
How to Use
1. Download the Dataset
Download the file 20200325_counsel_chat.csv from the original repository:
🔗 https://github.com/nbertagnolli/counsel-chat/tree/master

This dataset contains scraped conversations from individuals seeking support from licensed therapists on counselchat.com.

After downloading, upload the CSV file to your Python environment. If you're using Google Colab, make sure to upload it after opening Healing_Space.ipynb.

2. Convert CSV to JSONL
Run Healing_Space.ipynb or Healing_Space.py up to the CSV to JSONL conversion section.
We’ll be uploading the generated .jsonl file to Google Cloud Storage.

In Google Cloud Console, go to Storage > Buckets.

Click the “Create” button to make a new bucket (e.g., name it counseling_data or any name you prefer).

Inside your new bucket, click “Upload Files” and upload the .jsonl file.

3. Supervised Fine-Tuning with Vertex AI
In Google Cloud Console, open the Navigation menu (☰).

Go to Vertex AI > Tuning.

Click “Create tuned model”.

Enter:

Model name: e.g., Healing Space

Base model: gemini-2.0-flash-lite-001

Region: us-central1 (Iowa)

(Optional) Click Advanced options to modify:

Epochs: 38

Learning rate multiplier: 1

Adapter size: 4

In the Tuning Dataset section, select the JSONL file you uploaded earlier.

Click “Start tuning”. This process usually takes around 20–25 minutes.

4. Connect the Fine-Tuned Model to Your Python Environment
Return to Healing_Space.ipynb or Healing_Space.py. In the “Connect a supervised model” section:

Update the following with your actual values:


aiplatform.init(project="your-project-id", location="your-region")
model_name = "projects/your-project-id/locations/your-region/models/your-model-id"
💡 You can find your project ID, region, and model ID in the Details section of your tuned model in Vertex AI.

5. Create an Endpoint
Run the second code block in the “Connect a supervised model” section. This will create an endpoint for your fine-tuned model.

6. Run the UI/UX
In the UI and UX section of the notebook or script:

Fill in the following lines with your details:

# Initialize Vertex AI
aiplatform.init(project="your-project-id", location="your-region")

# Load your fine-tuned AI Therapist model
tuned_model = GenerativeModel(model_name="projects/your-project-id/locations/your-region/endpoints/your-endpoint-id")
Run the entire UI and UX section to launch the AI therapist web interface.

