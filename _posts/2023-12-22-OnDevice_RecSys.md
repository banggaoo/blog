---
title: "OnDevice RecSys"
date: 2023-12-22
tags: [AI, RecSys]
---
## Purpose
Developing a recommendation system that rearranges content rankings locally.

Reviewing OnDevice AI app.

## Specifications
Exposure of feedback component when user returns after selecting content.

When you select like/dislike in the feedback component, the information is stored in the ranking system.

Rearrange the list of content waiting to be exposed in the recommendation system just before new content is exposed.

Displayed in order of highest rank among the rearranged content list.

## Design
Predict content you might like using Linear Regression.

Train in real time on OnDevice using CreateML.

Convert content information including like/dislike feedback into tabular data and use it as learning information.

Immediately predicts after learning and rearranges the list of content waiting to be exposed.

To prevent unnecessary inference work, predictions are re-performed only when feedback information changes.

## Implementation
Create a Regressor during inference to sequentially execute learning and prediction.

```swift
    func computeRecommendations(basedOn items: [Likable<Content>]) async throws -> [Content] {
        return try await withCheckedThrowingContinuation { continuation in
            queue.async {
                let trainingData = items.filter {
                    $0.isLiked != nil
                }
                
                let trainingDataFrame = self.dataFrame(for: trainingData)
                
                let testData = items
                let testDataFrame = self.dataFrame(for: testData)
                
                do {
                    let regressor = try MLLinearRegressor(trainingData: trainingDataFrame, targetColumn: "like")
                    
                    let predictionsColumn = (try regressor.predictions(from: testDataFrame)).compactMap { value in
                        value as? Double
                    }
                    
                    let sorted = zip(testData, predictionsColumn)
                        .sorted { lhs, rhs -> Bool in
                            lhs.1 > rhs.1
                        }
                        .filter {
                            $0.1 > 0
                        }
                        .prefix(10)
                                        
                    let result = sorted.map(\.0.model)
                    
                    continuation.resume(returning: result)
                } catch {
                    continuation.resume(throwing: error)
                }
            }
        }
```

## Test
Dislike feedback applied to dating/broadcast content after content exposure.

As a result of checking the lowest ranking after applying 5 feedbacks, it was confirmed that the ranking of the broadcast content decreased.

## Examine
You can do something similar with [MLRecommender](https://developer.apple.com/documentation/createml/mlrecommender) from Apple, but only on MacOS.

Feedback information must be stored in the Persistent Store to maintain feedback data even when the app instance is terminated and restarted.

In the case of OnDevice ranking, it is expected to be free from personal information protection laws, so events that occur throughout the app can be collected and applied to services within the app.

Assuming an app is adopted OnDevice personalized recommendations gradually, storing user interest information in the Persistant Store in advance is expected to be helpful in providing future features.

Use App Groups for sharing app feedback data between company's OnDevice RecSys-powered apps, enhancing the overall recommendation experience.
