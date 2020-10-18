# The Are of Readable Code by Dustin Boswell

## Chapter 4: Aesthetics

### Key Summary

- Use consistent layout, with patterns the reader can get used to.
- Make similar code look similar.
- Group related lines of code into blocks.

Consistentency and packaging relating codes together is the new aesthetics. 

**We are almost ready to Go.**

### Note

#### What is Aesthetics?

Aesthetics is how it feels to read your code.

- Is it clean?
- Is it consistent?
- Is it easy to understood for others?
- Is it pleasant to read?
- It is often **VISUAL** instead of logics

#### Rearrange Line Breaks to Be Consistent and Compact

Carefully use line breaks to rearrange codes, so that the same level codes have the same indent.

```golang
apiLogger :=
    log.WithFields(log.Fields{
        "path": c.FullPath(),
    })
DemonSlayerKimetsuNoYaibaLogger :=
    log.WithFields(log.Fields{
        "path": c.FullPath(),
    })
superSaiyanApiLogger :=
    log.WithFields(log.Fields{
        "path": c.FullPath(),
    })
```

is way better than

```golang
apiLogger := log.WithFields(log.Fields{
            "path": c.FullPath(),
        })
DemonSlayerKimetsuNoYaibaLogger := log.WithFields(log.Fields{
            "path": c.FullPath(),
        })
superSaiyanApiLogger := log.WithFields(log.Fields{
            "path": c.FullPath(),
        })
```

#### Use Methods to Clean Up Irregularity

In Go, we have a evil boilerplate.

```golang
f, err := os.Open("filename.ext")
if err != nil {
    log.Fatal(err)
}

if err := a(); err != nil {
  return fmt.Errorf("doing a stuff: %v", err)
}
```

It's annoying but necessary. Also it's consistent and it's already an unfortunate idiom, so it's hard to break.

A way to improve it is to introduce an additional method to check the `err`.

```golang
func IsError(err error) bool {
   return err
}

f, err := os.Open("filename.ext")
if IsError(err) {
    log.Fatal(err)
}
```

We may even go furthur

```golang
func IsNil(i interface{}) bool {
   return i == nil
}

f, err := os.Open("filename.ext")
if IsNil(err) {
    log.Fatal(err)
}
```

Furthurmore, we may hide some error state handling in the method.

Like validation or assertion.

#### Use Column Alignment When Helpful

In Golang, the de factor way is to use `gofmt` to format code. Parameters alignment is not possible in golang unless you turn off code formatter, which it not ideal.

However column alignment is everywhere in Golang world.

```golang
type Options struct {
    ChannelID  string `form:"channelId"`  // For YouTube
    EventType  string `form:"eventType"`  // For YouTube
    IDs        string `form:"id"`         // For YouTube
    MaxResults int64  `form:"maxResults"` // For YouTube
}
```

is an example for column alignment. Types, tags, and comments are all aligned, and it's pleasant to read.

#### Pick a Meaningful Order, and Use It Consistently

This is another good principle, but it's often neglected. We just add new constant, variable, or function to the buttom of the pile due to the fear of cluttering the codes.

However, as a professional developer, as we are adding new codes, we should understand the code. Putting your code to the buttom of the pile is just an lazy way, and we should do our best to avoid it.

#### Organize Declarations into Blocks

This is an example from a great open source project, `cfssl`.

```golang
type Accessor interface {
    InsertCertificate(cr CertificateRecord) error
    GetCertificate(serial, aki string) ([]CertificateRecord, error)
    GetUnexpiredCertificates() ([]CertificateRecord, error)
    GetRevokedAndUnexpiredCertificates() ([]CertificateRecord, error)
    GetRevokedAndUnexpiredCertificatesByLabel(label string) ([]CertificateRecord, error)
    RevokeCertificate(serial, aki string, reasonCode int) error
    InsertOCSP(rr OCSPRecord) error
    GetOCSP(serial, aki string) ([]OCSPRecord, error)
    GetUnexpiredOCSPs() ([]OCSPRecord, error)
    UpdateOCSP(serial, aki, body string, expiry time.Time) error
    UpsertOCSP(serial, aki, body string, expiry time.Time) error
}
```

To organize it into blocks, we have...

```golang
type Accessor interface {

    // Modify Certificate
    InsertCertificate(cr CertificateRecord) error
    RevokeCertificate(serial, aki string, reasonCode int) error

    // Get Certificate
    GetCertificate(serial, aki string) ([]CertificateRecord, error)
    GetUnexpiredCertificates() ([]CertificateRecord, error)
    GetRevokedAndUnexpiredCertificates() ([]CertificateRecord, error)
    GetRevokedAndUnexpiredCertificatesByLabel(label string) ([]CertificateRecord, error)

    // Modify OCSP
    InsertOCSP(rr OCSPRecord) error
    UpdateOCSP(serial, aki, body string, expiry time.Time) error
    UpsertOCSP(serial, aki, body string, expiry time.Time) error
    
    // Get OCSP
    GetOCSP(serial, aki string) ([]OCSPRecord, error)
    GetUnexpiredOCSPs() ([]OCSPRecord, error)
}
```

#### Break Code into “Paragraphs”

Write the codes as if you are writing an article. Provide a meaningful flow, ergo a more clear purpose.

Empty line to break the block and comments are useful tool for it.

#### Personal Style versus Consistency

In Golang, a lot of style has convention and the convention is often mandatory.

However, there's still room for personal style.

Coding style is no way to be "wrong" for me. Maintain a consistant coding is always more important that to deviate from it for personal "right" style.

#### One more thing

It's basic but sometime it's forgotten by our fellow peers.

No more 80 characters in one line. A new trending standard is no more than 120 characters in one line.
