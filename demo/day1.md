Step 1: Enable Service
    Enable Google Cloud Vision API 
    -- gcloud services enable vision.googleapis.com
Step 2: Create Bucket uploaded-pictures-{PROJECT-ID}
Step 3: Set Permission allUsers
Step 5: Create Firestore Database
Step 4: Create Function picture-uploaded

Step 6: Create thumbnails Bucket
Step 7: Clone Code
    -- git clone https://github.com/kienle8475/demo-cloud-day-1-serverless.git
Step 8: Create and publish container image
    -- gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT/thumbnail-service
Step 9: Set the Cloud Run region to one of the supported regions and platform to managed:
    -- gcloud config set run/region us-west1
    -- gcloud config set run/platform managed

Step 10: Deploy on GCP Cloud Run
    --  SERVICE_NAME=thumbnail-service
        gcloud run deploy $SERVICE_NAME \
            --image gcr.io/$GOOGLE_CLOUD_PROJECT/thumbnail-service \
            --update-env-vars BUCKET_THUMBNAILS=$BUCKET_THUMBNAILS



Step 11: Create Topic Pub/Sub 
    -- TOPIC_NAME=cloudstorage-cloudrun-topic
    -- gcloud pubsub topics create $TOPIC_NAME

TOPIC_NAME = cloudstorage-cloudrun-topic
BUCKET_PICTURES = uploaded-pictures-{PROJECT-ID}
SERVICE_ACCOUNT = cloudstorage-cloudrun-topic-sa

Step 12: Create Pub/Sub notification
    -- gsutil notification create -t cloudstorage-cloudrun-topic -f json gs://$BUCKET_PICTURES
Step 13: Create Service Account
    -- gcloud iam service-accounts create cloudstorage-cloudrun-topic-sa  --display-name "Cloud Run Pub/Sub Invoker"
Step 14: Set service account invoker Cloud Run 

