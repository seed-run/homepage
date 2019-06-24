---
layout: build-errors
title: Stack is in state and can not be updated
image: /assets/social-cards/common-errors.png
description: "Stack:arn:aws:cloudformation:us-xxxx-x:xxxxxxxxx:stack/xxx-xx-prod/xxxx-xxxx-xxxx-xxxx-xxxx is in ROLLBACK_FAILED state and can not be updated."
---

#### Error Message

> Stack:arn:aws:cloudformation:us-xxxx-x:xxxxxxxxx:stack/xxx-xx-prod/xxxx-xxxx-xxxx-xxxx-xxxx is in ROLLBACK_FAILED state and can not be updated.


#### Problem

The CloudFormation stack is in a busy or error state, and the new deployment has been rejected by CloudFormation. 

#### Solution

The solution depends on the specific state that your CloudFormation stack is in.

- _CREATE_IN_PROGRESS_

  The stack is currently being created. You cannot deploy until the creation is completed. You need to wait until the process completes.

- _UPDATE_IN_PROGRESS_

  The stack is currently being updated. You cannot make another update if one is currently in progress. You need to wait. If you don't want to proceed with the update, you can cancel the update, and the stack will be rolled back to the working state prior to the update.

- _UPDATE_COMPLETE_CLEANUP_IN_PROGRESS_

  The stack has been updated, and CloudFormation is cleaning up the old resources that are no longer needed. For example, when you update resources that require to be replaced, CloudFormation creates the new resources first and then deletes the old resources to help reduce any interruptions. In this state, the stack has been updated and is usable, but CloudFormation is still deleting the old resources. You need to wait for this to complete.

- _UPDATE_ROLLBACK_IN_PROGRESS_

  The stack failed to update or the update has been canceled. CloudFormation is rolling back the stack to its previous working state. You've to wait until the rollback completes.

- _UPDATE_ROLLBACK_COMPLETE_CLEANUP_IN_PROGRESS_

  The stack failed to update, CloudFormation rolled back the stack to its previous working state, and is cleaning up the resources that are no longer needed. You've to wait for the rollback process to complete.

- _UPDATE_ROLLBACK_FAILED_

  The stack failed to update, and CloudFormation failed to rollback to its previous working state. In this state, you cannot make further deployments. To get the stack working again, go to your CloudFormation console and see what caused the rollback failure. Fix the failure and try to continue the rollback process. Or, if deleting the stack and starting over is an option, consider doing so.

- _DELETE_IN_PROGRESS_

  The stack is currently being deleted. You cannot deploy until the delete is complete. You'll need to wait for this process to complete.

- _DELETE_FAILED_

  The stack failed to delete. In this state, you cannot make further deployments. Go to your CloudFormation console and see what caused the failure. Fix the failure and try removing the stack again.
