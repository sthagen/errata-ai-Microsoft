# Microsoft

> **NOTE**: This project is neither maintained nor endorsed by Microsoft.

This repository contains a [Vale-compatible](https://github.com/errata-ai/vale) implementation of the [*Microsoft Writing Style Guide*](https://docs.microsoft.com/en-us/style-guide/welcome/) ([LICENSE](https://github.com/MicrosoftDocs/microsoft-style-guide/blob/master/LICENSE)).

## Getting started

To get started, add the package to your configuration file (as shown below) and then run `vale sync`.

```ini
StylesPath = styles
MinAlertLevel = suggestion

Packages = Microsoft

[*]
BasedOnStyles = Vale, Microsoft
```

See [Packages](https://vale.sh/hub/microsoft/) for more information.

## Repository structure

<dl>
  <dt><a href="https://github.com/errata-ai/Microsoft/tree/master/Microsoft"><code>/Microsoft</code></a></dt>
  <dd>The <a href="http://yaml.org/">YAML</a>-based rule implementations that make up our style.</dd>

  <dt><a href="https://github.com/errata-ai/Microsoft/tree/master/fixtures"><code>/fixtures</code></a></dt>
  <dd>The individual unit tests. Each directory should be named after a rule found in <code>/Microsoft</code> and include its own <code>.vale.ini</code> file that isolates its target rule.</dd>

  <dt><a href="https://github.com/errata-ai/Microsoft/tree/master/testdata"><code>/testdata</code></a></dt>
  <dd>The expected Vale output for each fixture directory, one <code>&lt;Rule&gt;.ct</code> file per fixture. We use <a href="https://github.com/google/go-cmdtest">go-cmdtest</a> to run Vale against each fixture and compare its output. Run the suite with <code>go test ./...</code>; regenerate the expectations after an intentional change with <code>go test ./... -update</code>.</dd>

  <dt><a href="https://github.com/errata-ai/Microsoft/tree/master/coverage"><code>/coverage</code></a></dt>
  <dd>How much of the style guide we implement, tracked topic by topic. Each file mirrors one top-level section of the guide, and each key is a subtopic set to <code>true</code> or <code>false</code>, optionally followed by a comment naming the rules that implement it.</dd>
</dl>

## Coverage

Run `go test -v -run TestCoverage ./...` to print the current figures:

```
  guidelines:     37/64 (57.8%)
  A-Z word list:  106/849 (12.5%)
```

The two are reported separately because the A–Z word list is roughly ten times
the size of everything else, so a single combined percentage tells you almost
nothing about the guidelines.

The same test enforces what keeps the number honest: values must be exactly
`true` or `false`, and every rule named in a comment must still exist. A rule
that's renamed or merged away therefore can't leave a topic silently claiming
coverage it no longer has.

Sections of the guide that describe process rather than prose have no manifest,
since there's nothing there for a linter to check: Checklists, Content planning,
Design planning, Final publishing review, Search and writing, and Top 10 tips.
Scannable content and Text formatting are also absent for now; their
lintable subtopics (headings, sentence-style capitalization) are already counted
under `capitalization.yml`, and listing them again would double-count.

## Extension points

| Check | Implementations |
|:---:|:---|
| [`existence`](https://vale.sh/docs/checks/existence) | [`AMPM.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/AMPM.yml), [`Accessibility.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Accessibility.yml), [`Adverbs.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Adverbs.yml), [`Auto.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Auto.yml), [`Avoid.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Avoid.yml), [`Dashes.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Dashes.yml), [`DateFormat.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/DateFormat.yml), [`DateNumbers.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/DateNumbers.yml), [`DateOrder.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/DateOrder.yml), [`Ellipses.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Ellipses.yml), [`ExclamationPoints.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/ExclamationPoints.yml), [`FirstPerson.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/FirstPerson.yml), [`Gender.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Gender.yml), [`GeneralURL.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/GeneralURL.yml), [`HeadingAcronyms.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/HeadingAcronyms.yml), [`HeadingColons.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/HeadingColons.yml), [`HeadingPunctuation.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/HeadingPunctuation.yml), [`Hyphens.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Hyphens.yml), [`Negative.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Negative.yml), [`Ordinal.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Ordinal.yml), [`OxfordComma.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/OxfordComma.yml), [`Passive.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Passive.yml), [`Percentages.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Percentages.yml), [`Plurals.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Plurals.yml), [`QuestionMarks.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/QuestionMarks.yml), [`Quotes.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Quotes.yml), [`RangeTime.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/RangeTime.yml), [`Semicolon.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Semicolon.yml), [`Spacing.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Spacing.yml), [`Suspended.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Suspended.yml), [`UIVerbs.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/UIVerbs.yml), [`Units.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Units.yml), [`Uppercase.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Uppercase.yml), [`Vocab.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Vocab.yml), [`We.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/We.yml) |
| [`substitution`](https://vale.sh/docs/checks/substitution) | [`BiasFree.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/BiasFree.yml), [`Contractions.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Contractions.yml), [`Foreign.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Foreign.yml), [`GenderBias.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/GenderBias.yml), [`Jargon.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Jargon.yml), [`Militaristic.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Militaristic.yml), [`Terms.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Terms.yml), [`URLFormat.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/URLFormat.yml), [`Wordiness.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Wordiness.yml) |
| [`occurrence`](https://vale.sh/docs/checks/occurrence) | [`SentenceLength.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/SentenceLength.yml) |
| [`repetition`](https://vale.sh/docs/checks/repetition) | N/A |
| [`consistency`](https://vale.sh/docs/checks/consistency) | N/A |
| [`capitalization`](https://vale.sh/docs/checks/capitalization) | [`Headings.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Headings.yml) |
| [`conditional`](https://vale.sh/docs/checks/conditional) | [`Acronyms.yml`](https://github.com/errata-ai/Microsoft/blob/master/Microsoft/Acronyms.yml) |
| [`metric`](https://vale.sh/docs/checks/metric) | N/A |
| [`spelling`](https://vale.sh/docs/checks/spelling) | N/A |
| [`sequence`](https://vale.sh/docs/checks/sequence) | N/A |
| [`script`](https://vale.sh/docs/checks/script) | N/A |
| [`readability`](https://vale.sh/docs/checks/readability) | N/A |


