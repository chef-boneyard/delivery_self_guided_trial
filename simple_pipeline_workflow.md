# Collaborative Pipeline Workflow

In [Local Development Cookbook workflow](simple_delivery_workflow.md) section we cloned a project, checked out a feature branch, created a change, tested it locally and submitted it for review into Delivery.

In this section we will make sure the Verify stage passes, after which we will Review the change collaboratively and Accept it. We can watch the change get merged into its Acceptance environment, after which we can Ship the change to be merged into master.

## pre-requisites

1. You followed the [Local Development Cookbook workflow](simple_delivery_workflow.md) guide and submitted a change for review by running `delivery review`.

## workflow
1. The `delivery review` command produced a URL to the pipeline. Open that URL in a browser (unless delivery has already done that for you). You should land on the Status page of your change, running the **Verify** stage. Make sure that the **Unit, Lint and Syntax** phases passed successfully. If any phase failed, click the failed phase to expand the log, troubleshoot and submit a fixing commit (Steps 4-8 of [Local Development Cookbook workflow](simple_delivery_workflow.md) ).

2. This is where the collaborative part comes in. We strongly advise that the person submitting the change should NOT be the person reviewing it. Hence, take the URL from the previous step and chat/email it to a teammate, asking them for a code review.

3. Change into the newly created project directory and create a new feature branch in the cloned project:

        cd sitedbaas
        git checkout -b "binamov/bestest-feature-ever"

4. Go ahead and make changes to the cookbook. Some of the easiest things to change are attribute values in `attributes/default.rb`. Don't forget to save the files you change.

5. Bump the cookbook version in `metadata.rb`

6. Stage your changes and commit them:

        git add .
        git commit -m "this is the best change ever!"

7. Run lint/unit/syntax tests locally first:

        delivery job verify lint
        delivery job verify unit
        delivery job verify syntax


8. You can now submit your change for Delivery review:

        delivery review
        # add an --no-open flag if you don't want the change to open in the WebUI

  *Pushes the change for review and opens browser to the change in the WebUI.*

#### [Continue in Delivery workflow](simple_delivery_workflow.md)
