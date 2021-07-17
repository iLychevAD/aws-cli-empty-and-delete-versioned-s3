https://stackoverflow.com/questions/29809105/how-do-i-delete-a-versioned-bucket-in-aws-s3-using-the-cli

### Delete versions:
aws s3api delete-objects \
    --bucket ${bucket} \
    --delete "$(aws s3api list-object-versions \
    --bucket ${bucket} \
    --output=json \
    --query='{Objects: Versions[].{Key:Key,VersionId:VersionId}}')"

### Then delete the delete markers:
aws s3api delete-objects \
    --bucket ${bucket} \
    --delete "$(aws s3api list-object-versions \
    --bucket ${bucket} \
    --output=json \
    --query='{Objects: DeleteMarkers[].{Key:Key,VersionId:VersionId}}')"
