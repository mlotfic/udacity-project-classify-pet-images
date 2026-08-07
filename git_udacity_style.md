# 📝 Git Development History

The project was developed incrementally using Git commits.

Example development history:

```text
Initial project setup
Add Conda environment configuration
Implement command line arguments
Implement pet image label extraction
Implement image classification
Implement dog classification comparison
Add execution time measurement
Add project rubric evidence screenshots
Document project and rubric verification
```
Document project and rubric verification
Add project rubric evidence screenshots
Add execution time measurement
Implement dog classification comparison
Implement image classification
Implement pet image label extraction
Implement command line arguments
Add Conda environment configuration
Initial project setup

I'd actually put the environment commit near the beginning, before the implementation commits, if you're rebuilding the repository history from scratch:

Initial project setup
Add Conda environment configuration
Implement command line arguments
Implement pet image label extraction
Implement image classification
Implement dog classification comparison
Add execution time measurement
Add project rubric evidence screenshots
Document project and rubric verification
This provides a traceable history from the initial project setup through implementation, testing, evidence collection, and final documentation.

---


```powershell
git status
```

and eventually:

```powershell
git add environment.yml
git commit -m "Add Conda environment configuration"
git push
```