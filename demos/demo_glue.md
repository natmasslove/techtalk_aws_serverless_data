

# Glue

## Running Glue Job
 - Browse to Glue -> Jobs -> job_name: gluej-techtalk-sample
 - Trigger the job, and while it's running
 - Explain parameters:
   - enable-metrics, enable-spark-ui, enable-observability-metrics
   - enable-auto-scaling
 - When run is completed:
   - Show S3 results
   - Show run info: "DPU Hours"
   - Show metrics & spark UI
 

## Running FLEX Glue Job
  - Choose Job "gluej-techtalk-sample-flex"
  - Show Job details -> FLEX execution
  - Show previous execution

## Glue Interactive Sessions (Jupyter Notebooks)

### Locally
  - Show how to run it Visual Studio
    - it opens in c:\_Garb\glue_interactive_sessions
    - load notebook tech_talk_demo_local.ipynb

 
### Inside the Glue Job AWS UI 
  - Service: Glue -> Jobs -> Notebook
  - load the same + role "role-techtalk-glue-notebook"
  - Show how it runs in Glue Job AWS UI
  - Auto conversion to your glue job

