---
cover: broken-reference
coverY: 0
---

# Phi 2.0 - Training Configuration

This is the default training configuration.  We will leave it as is for the time being.

```yaml
gradient_accumulation_steps: 4
micro_batch_size: 2
num_epochs: 4
optimizer: adamw_bnb_8bit
lr_scheduler: cosine
learning_rate: 0.0002
```
