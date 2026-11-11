# Kuza AI Data and Testing Guide

**Owner:** Hashimweyesu Jean de Dieu  
**Status:** Draft for team review

1. **Record each image source.** Note where the images came from, allowed uses, crop, labels and known limitations. Confirm permission before using farmer photos for training.
2. **Prepare the images.** Review unclear labels with Eunice and remove duplicates. Keep related images from the same plant or field together where that information is available.
3. **Split the data.** Use one set to train, another to choose thresholds and a separate set for final testing. Record the split and keep final test images out of training and threshold selection.
4. **Test the exact model version.** For each condition, record image count, correct flags, false flags, missed cases and uncertain results. Include blurry and unfamiliar images to check retake and uncertainty behavior.
5. **Approve a release.** Record which conditions passed the agreed checks. Use the uncertain result for conditions without enough evidence. Keep the previous model version available if the new one performs worse.

For sample retraining, record the data version, settings, steps, resulting model version and comparison with the previous results. Jean fills in the dataset names, test counts and approval thresholds after review.
