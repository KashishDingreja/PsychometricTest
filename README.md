# PsychometricTest

# AI-Based Psychometric Assessment System

An AI-powered psychometric assessment application that combines text-based
personality classification with facial emotion analysis to provide MBTI and
OCEAN personality insights.

## Overview

This project explores a multimodal approach to personality assessment by
combining:

- BERT-based natural language processing for MBTI classification
- Real-time facial emotion recognition using DeepFace
- OpenCV-based webcam processing
- OCEAN personality trait estimation
- Flask-based web application and result visualization

The system provides two complementary assessment workflows:

1. Text-based MBTI assessment
2. Webcam-based facial emotion and OCEAN assessment

## Features

### MBTI Personality Classification

The application presents a personality questionnaire and processes the
responses using a BERT-based classification pipeline.

The model:

- Uses `bert-base-uncased`
- Tokenizes and pads questionnaire responses
- Uses attention masks and token type IDs
- Extracts contextual representations using BERT
- Performs multi-label classification across four MBTI dimensions:
  - Introversion / Extraversion (I/E)
  - Intuition / Sensing (N/S)
  - Thinking / Feeling (T/F)
  - Judging / Perceiving (J/P)

The four predictions are combined to generate the final MBTI type.

### Facial Emotion & OCEAN Analysis

The application can access the user's webcam and perform real-time facial
emotion analysis.

The pipeline uses:

OpenCV → Face Detection → DeepFace Emotion Recognition
→ Emotion Aggregation → OCEAN Trait Estimation

Detected emotions are mapped to five OCEAN personality dimensions:

- Openness
- Conscientiousness
- Extraversion
- Agreeableness
- Neuroticism

The resulting scores are visualized using a generated personality chart.

## System Architecture

```text
                    ┌─────────────────────┐
                    │    Flask Web App    │
                    └──────────┬──────────┘
                               │
              ┌────────────────┴────────────────┐
              │                                 │
              ▼                                 ▼
     ┌──────────────────┐             ┌──────────────────┐
     │ MBTI Assessment  │             │ OCEAN Assessment │
     └────────┬─────────┘             └────────┬─────────┘
              │                                 │
              ▼                                 ▼
       Questionnaire                    Webcam Input
              │                                 │
              ▼                                 ▼
       Text Preprocessing                 OpenCV Face
              │                            Detection
              ▼                                 │
        BERT Tokenizer                           ▼
              │                           DeepFace
              ▼                           Emotion Model
        BERT Encoder                             │
              │                                 ▼
              ▼                         Emotion Aggregation
       4 MBTI Outputs                            │
              │                                 ▼
              ▼                         OCEAN Estimation
        MBTI Result                              │
                                                ▼
                                         Visualization
