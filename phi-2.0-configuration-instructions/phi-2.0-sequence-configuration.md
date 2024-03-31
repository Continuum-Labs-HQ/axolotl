---
cover: broken-reference
coverY: 0
---

# Phi 2.0 - Sequence Configuration

Before training or fine-tuning begins, the <mark style="color:yellow;">input data must be correctly formatted and prepared</mark>.

We will be configuring the:

Sequence Length

1. Sequence Length
2. Sample Packing
3. Padding to Sequence

```yaml
sequence_len: 4096
sample_packing: true
pad_to_sequence_len: true
```

### <mark style="color:blue;">sequence\_len</mark>

This parameter sets the <mark style="color:yellow;">maximum allowable length for input sequences</mark>. Sequences longer than this length may be truncated or split during training.

&#x20;This limit is essential since transformers process input data in fixed-size blocks.

Sequences longer than this length are either truncated or split. Truncation means cutting off the part of the sequence that exceeds the limit, while splitting involves dividing a long sequence into smaller segments, each within the maximum length.

The choice of sequence length affects memory usage and computational requirements. Longer sequences can capture more context but require more computational resources.

### <mark style="color:blue;">sample\_packing</mark>

A flag that determines whether sample packing should be used.&#x20;

This is a method to optimize the training process by packing multiple shorter sequences into a single training example (batch).  It can increases training efficiency by reducing padding needs and better utilizing GPU memory. This technique is particularly useful when dealing with variable-length sequences.

**Implementation**: If set to <mark style="color:yellow;">`true`</mark>, sequences that are shorter than <mark style="color:yellow;">`sequence_len`</mark> are concatenated with others to form a packed batch. This process continues until the maximum sequence length is reached or no more sequences are available for packing.

### <mark style="color:blue;">pad\_to\_sequence\_len</mark>

This is a flag that controls whether sequences should be padded to match the specified sequence length.

This ensures that <mark style="color:yellow;">all sequences in a batch are of the same length</mark>, which is necessary for parallel processing by the model.   Shorter sequences are extended (padded) with special tokens (usually `[PAD]`) to reach the defined maximum sequence length.

Padding is a standard practice in training neural networks on sequences of varying lengths, but it can introduce additional computational overhead, especially with longer sequence lengths.

If set to "true," input sequences will be padded with special tokens to reach the maximum sequence length defined earlier.
