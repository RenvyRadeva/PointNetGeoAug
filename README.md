# Abstract
LiDAR sensors play a pivotal role in acquiring essential data in the form of 3D point clouds. The majority of prior studies have experimented with synthetic datasets containing precisely aligned data, while real world point clouds are often not aligned and iregular. The iregularity of LiDAR-generated point clouds poses challenges, particularly in transformation invariance and points iregularity. To address this, geometric transformation-based data augmentation is employed to enhance the PointNet model's ability to recognize objects with varying iregular points and transformation. The proposed methodology aims to improve the classification of 3D objects in LiDAR-scanned objects, enhancing the adaptability and robustness of models in real-world scenarios by combining a local and global jitter, rotation, and scale data augmentation to ModelNet40. In results, the augmented model exhibits a notable performance enhancement and resilience against rotational disturbances in the upper coordinates. The augmented model demonstrates a validation accuracy of 80.1% with randomly applied transformations while the highest transformation variation is rotation on the up axis, whereas the non-augmented model achieves an accuracy of 45.5%.

# Results
| Model                 | Aligned            | Transformed        | Transformed Normalized Rotation |
|-----------------------|--------------------|--------------------|---------------------------------|
| Non-Augmented         | 84.8%              | 45.5%              | 45.5%                           |
| Augmented (100)       | 77.5%              | 77.5%              | 77.3%                           |
| Augmented (200)       | 82.0%              | 80.1%              | 80.3%                           |

# LiDAR Cropped Classification
<img width="444" alt="image" src="https://github.com/RenvyRadeva/PointNetGeoAug/assets/42593819/870e08cf-cb6d-4612-a029-0d45477de986">

| Model               | chair_01 | chair_02 | chair_03 | plant_01 | plant_02 | plant_03 | pot   | toilet |
|---------------------|----------|----------|----------|----------|----------|----------|-------|--------|
| Non-Augmented       | chair    | bed      | stairs   | plant    | plant    | plant    | toilet| stairs |
| Augmented (100)     | chair    | chair    | chair    | plant    | toilet   | plant    | cup   | toilet |
| Augmented (200)     | chair    | chair    | chair    | plant    | plant    | plant    | cup   | toilet |

# Conclusion
Since LiDAR data frequently exhibit high rotation variations along the up axis, this works employs rotation data augmentation with a maximum of 180 degrees along the up axis. Meanwhile, minimal variation values are applied in other coordinates. In terms of rotational invariance, it appears that data augmentation effectively aids the model in better handling rotation variations. However, for global and local jitter methods, it is observed that the model without augmentation demonstrates higher accuracy compared to the augmented model. Furthermore, there is an observable increase in accuracy for the augmented model when dealing with data of varying scales.

In the lidar test data, it is evident that the model encounters difficulty in detecting pot-shaped objects. This challenge may arise due to the ambiguity in the shapes of objects resembling cups or flower vases. Additionally, it could be attributed to data acquisition that still contains noise outside the object shapes, resulting in the model struggling to provide accurate predictions.
