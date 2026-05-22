# Reference
<details><summary><code>client.Parse(request) -> *extend.ParseRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Parse a file synchronously, waiting for the result before returning. This endpoint has a **5-minute timeout** — if processing takes longer, the request will fail.

**Note:** This endpoint is intended for onboarding and testing only. For production workloads, use `POST /parse_runs` with [polling or webhooks](https://docs.extend.ai/2026-02-09/developers/async-processing) instead, as it provides better reliability for large files and avoids timeout issues.

The Parse endpoint allows you to convert documents into structured, machine-readable formats with fine-grained control over the parsing process. This endpoint is ideal for extracting cleaned document content to be used as context for downstream processing, e.g. RAG pipelines, custom ingestion pipelines, embeddings classification, etc.

For more details, see the [Parse File guide](https://docs.extend.ai/2026-02-09/product/parsing/parse).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ParseRequest{
        File: &extend.ParseRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/bank_statement.pdf",
                Name: extend.String(
                    "bank_statement.pdf",
                ),
            },
        },
    }
client.Parse(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**responseType:** `*extend.ParseRequestResponseType` 

Controls the format of the response chunks. Defaults to `json` if not specified.
* `json` - Returns parsed outputs in the response body
* `url` - Return a presigned URL to the parsed content in the response body
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.ParseRequestFile` — The file to be parsed. Files can be provided as a URL or an Extend file ID.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ParseConfig` 
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Edit(request) -> *extend.EditRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Edit a file synchronously, waiting for the result before returning. This endpoint has a **5-minute timeout** — if processing takes longer, the request will fail.

**Note:** This endpoint is intended for onboarding and testing only. For production workloads, use `POST /edit_runs` with [polling or webhooks](https://docs.extend.ai/2026-02-09/developers/async-processing) instead, as it provides better reliability for large files and avoids timeout issues.

The Edit endpoint allows you to detect and fill form fields in PDF documents.

For more details, see the [Edit File guide](https://docs.extend.ai/2026-02-09/product/editing/edit).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EditRequest{
        File: &extend.EditRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/form.pdf",
            },
        },
        Config: &extend.EditConfig{
            Instructions: extend.String(
                "Fill out the form with the provided data",
            ),
            AdvancedOptions: &extend.EditConfigAdvancedOptions{
                FlattenPdf: extend.Bool(
                    true,
                ),
            },
        },
    }
client.Edit(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `*extend.EditRequestFile` — The file to be edited. Files can be provided as a URL or an Extend file ID.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.EditConfig` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Extract(request) -> *extend.ExtractRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Extract structured data from a file synchronously, waiting for the result before returning. This endpoint has a **5-minute timeout** — if processing takes longer, the request will fail.

**Note:** This endpoint is intended for onboarding and testing only. For production workloads, use `POST /extract_runs` with [polling or webhooks](https://docs.extend.ai/2026-02-09/developers/async-processing) instead, as it provides better reliability for large files and avoids timeout issues.

The Extract endpoint allows you to extract structured data from files using an existing extractor or an inline configuration.

For more details, see the [Extract File guide](https://docs.extend.ai/2026-02-09/product/extraction/quick-start-5-minutes).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractRequest{
        Config: &extend.ExtractConfigJSON{
            Schema: map[string]any{
                "properties": map[string]any{
                    "invoice_number": map[string]any{
                        "description": "The invoice number",
                        "type": "string",
                    },
                    "total_amount": map[string]any{
                        "description": "The total amount due",
                        "type": "number",
                    },
                    "vendor_name": map[string]any{
                        "description": "The name of the vendor",
                        "type": "string",
                    },
                },
                "type": "object",
            },
        },
        File: &extend.ExtractRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/invoice.pdf",
            },
        },
    }
client.Extract(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extractor:** `*extend.ExtractRequestExtractor` — Reference to an existing extractor. One of `extractor` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ExtractConfigJSON` — Inline extract configuration. One of `extractor` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.ExtractRequestFile` — The file to be extracted from. Files can be provided as a URL, Extend file ID, or raw text.
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Classify(request) -> *extend.ClassifyRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Classify a document synchronously, waiting for the result before returning. This endpoint has a **5-minute timeout** — if processing takes longer, the request will fail.

**Note:** This endpoint is intended for onboarding and testing only. For production workloads, use `POST /classify_runs` with [polling or webhooks](https://docs.extend.ai/2026-02-09/developers/async-processing) instead, as it provides better reliability for large files and avoids timeout issues.

The Classify endpoint allows you to classify documents using an existing classifier or an inline configuration.

For more details, see the [Classify File guide](https://docs.extend.ai/2026-02-09/product/classification/configuring-a-classifier).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifyRequest{
        Config: &extend.ClassifyConfig{
            Classifications: []*extend.Classification{
                &extend.Classification{
                    ID: "invoice",
                    Type: "invoice",
                    Description: "An invoice or bill for goods or services",
                },
                &extend.Classification{
                    ID: "receipt",
                    Type: "receipt",
                    Description: "A receipt confirming payment",
                },
                &extend.Classification{
                    ID: "other",
                    Type: "other",
                    Description: "Any other document type",
                },
            },
        },
        File: &extend.ClassifyRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/document.pdf",
            },
        },
    }
client.Classify(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classifier:** `*extend.ClassifyRequestClassifier` — Reference to an existing classifier. One of `classifier` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ClassifyConfig` — Inline classify configuration. One of `classifier` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.ClassifyRequestFile` — The file to be classified. Files can be provided as a URL, an Extend file ID, or raw text.
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Split(request) -> *extend.SplitRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Split a document synchronously, waiting for the result before returning. This endpoint has a **5-minute timeout** — if processing takes longer, the request will fail.

**Note:** This endpoint is intended for onboarding and testing only. For production workloads, use `POST /split_runs` with [polling or webhooks](https://docs.extend.ai/2026-02-09/developers/async-processing) instead, as it provides better reliability for large files and avoids timeout issues.

The Split endpoint allows you to split documents into multiple parts using an existing splitter or an inline configuration.

For more details, see the [Split File guide](https://docs.extend.ai/2026-02-09/product/splitting/configuring-a-splitter).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitRequest{
        Config: &extend.SplitConfig{
            SplitClassifications: []*extend.SplitClassification{
                &extend.SplitClassification{
                    ID: "invoice",
                    Type: "invoice",
                    Description: "An invoice or bill for goods or services",
                    IdentifierKey: extend.String(
                        "invoice number from the document header",
                    ),
                },
                &extend.SplitClassification{
                    ID: "receipt",
                    Type: "receipt",
                    Description: "A receipt confirming payment",
                    IdentifierKey: extend.String(
                        "receipt number",
                    ),
                },
                &extend.SplitClassification{
                    ID: "other",
                    Type: "other",
                    Description: "Any other document type",
                },
            },
        },
        File: &extend.SplitRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/multi-document.pdf",
            },
        },
    }
client.Split(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**splitter:** `*extend.SplitRequestSplitter` — Reference to an existing splitter. One of `splitter` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.SplitConfig` — Inline splitter configuration. One of `splitter` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.SplitRequestFile` — The file to be split. Files can be provided as a URL or an Extend file ID.
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Files
<details><summary><code>client.Files.List() -> *extend.FilesListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List files.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.FilesListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.Files.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**nameContains:** `*string` 

Filters files to only include those that contain the given string in the name.

Example: `"invoice"`
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Files.Retrieve(ID) -> *extend.File</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetch a file by its ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.FilesRetrieveRequest{}
client.Files.Retrieve(
        context.TODO(),
        "file_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

ID for the file. It will always start with `"file_"`.

Example: `"file_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**rawText:** `*bool` 

**Deprecated:** Use `POST /parse_runs` instead to parse file contents.

If set to true, the raw text content of the file will be included in the response.
    
</dd>
</dl>

<dl>
<dd>

**markdown:** `*bool` 

**Deprecated:** Use `POST /parse_runs` instead to parse file contents.

If set to true, the markdown content of the file will be included in the response.

Only available for files with a type of PDF, IMG, or DOCX files that were auto-converted to PDFs.
    
</dd>
</dl>

<dl>
<dd>

**html:** `*bool` 

**Deprecated:** Use `POST /parse_runs` instead to parse file contents.

If set to true, the html content of the file will be included in the response.

Only available for files with a type of DOCX.
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Files.Delete(ID) -> *extend.FilesDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a file and all associated data from Extend. This operation is permanent and cannot be undone.

This endpoint can be used if you'd like to manage data retention on your own rather than automated data retention policies. Or make one-off deletions for your downstream customers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.FilesDeleteRequest{}
client.Files.Delete(
        context.TODO(),
        "file_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the file to delete.

Example: `"file_xK9mLPqRtN3vS8wF5hB2cQ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Files.Upload(request) -> *extend.File</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Upload and create a new file in Extend.

This endpoint accepts file contents and registers them as a File in Extend, which can be used for [running workflows](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/workflow/create-workflow-run), [creating evaluation set items](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/evaluation/create-evaluation-set-item), [parsing](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/parse/parse-file), etc.

If an uploaded file is detected as a Word or PowerPoint document, it will be automatically converted to a PDF.

Supported file types can be found [here](https://docs.extend.ai/2026-02-09/product/general/supported-file-types).

This endpoint requires multipart form encoding. Most HTTP clients will handle this encoding automatically (see the examples).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.FilesUploadRequest{}
client.Files.Upload(
        context.TODO(),
        strings.NewReader(
            "",
        ),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**convertToPdf:** `*bool` — When true, converts the uploaded file to PDF. Supported file types include images (JPEG, PNG, TIFF, GIF, BMP, WebP, HEIC/HEIF), Word documents, PowerPoint, Excel, and HTML.
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ParseRuns
<details><summary><code>client.ParseRuns.List() -> *extend.ParseRunsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List parse runs, with optional filters for status, batch ID, source, and file name.

Returns a paginated list of parse runs. Use `GET /parse_runs/{id}` to retrieve the full result including output for a specific run.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ParseRunsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.ParseRuns.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `*extend.ParseRunsListRequestStatus` — Filter parse runs by status.
    
</dd>
</dl>

<dl>
<dd>

**batchID:** `*string` 

Filter parse runs by the batch they belong to. Use this after submitting a batch via `POST /parse_runs/batch` to retrieve individual run results.

Example: `"bpar_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**source:** `*extend.ParseRunSource` 

Filters parse runs by the source that created them. If not provided, runs from all sources are returned.

**Note:** When `batchId` is provided, it takes precedence and this filter is ignored.
    
</dd>
</dl>

<dl>
<dd>

**sourceID:** `*extend.RunSourceID` — Filters runs by the source ID.
    
</dd>
</dl>

<dl>
<dd>

**fileNameContains:** `*string` 

Filters runs by the name of the file. Only returns runs where the file name contains this string.

Example: `"invoice"`
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ParseRuns.Create(request) -> *extend.ParseRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Parse files to get cleaned, chunked target content (e.g. markdown).

The Parse endpoint allows you to convert documents into structured, machine-readable formats with fine-grained control over the parsing process. This endpoint is ideal for extracting cleaned document content to be used as context for downstream processing, e.g. RAG pipelines, custom ingestion pipelines, embeddings classification, etc.

The request returns immediately with a `PROCESSING` status. Use webhooks or poll the Get Parse Run endpoint for results.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ParseRunsCreateRequest{
        File: &extend.ParseRunsCreateRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/bank_statement.pdf",
                Name: extend.String(
                    "bank_statement.pdf",
                ),
            },
        },
    }
client.ParseRuns.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `*extend.ParseRunsCreateRequestFile` — The file to be parsed. Files can be provided as a URL or an Extend file ID.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ParseConfig` 
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ParseRuns.Retrieve(ID) -> *extend.ParseRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve the status and results of a parse run.

Use this endpoint to get results for a parse run that has already completed, or to check on the status of a parse run initiated by the [Create Parse Run](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/parse/create-parse-run) endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ParseRunsRetrieveRequest{}
client.ParseRuns.Retrieve(
        context.TODO(),
        "parse_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier for the parse run.

Example: `"pr_xK9mLPqRtN3vS8wF5hB2cQ"`
    
</dd>
</dl>

<dl>
<dd>

**responseType:** `*extend.ParseRunsRetrieveRequestResponseType` 

Controls how the output is delivered. Defaults to `inline`.
* `json` - Returns the output directly in the `output` field of the response body.
* `url` - Returns a presigned URL in the `outputUrl` field to download the output as a JSON file. The URL expires after 15 minutes. Useful for large outputs.
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ParseRuns.Delete(ID) -> *extend.ParseRunsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a parse run and all associated data from Extend. This operation is permanent and cannot be undone.

This endpoint can be used if you'd like to manage data retention on your own rather than automated data retention policies. Or make one-off deletions for your downstream customers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ParseRunsDeleteRequest{}
client.ParseRuns.Delete(
        context.TODO(),
        "parse_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the parse run to delete.

Example: `"pr_xK9mLPqRtN3vS8wF5hB2cQ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ParseRuns.CreateBatch(request) -> *extend.BatchRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit up to **1,000 files** for parsing in a single request. Each file is processed as an independent parse run using the same configuration.

Unlike the single [Parse File (Async)](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/parse/create-parse-run) endpoint, this batch endpoint accepts an `inputs` array and immediately returns a `BatchRun` object containing a batch `id` and a `PENDING` status. The individual runs are then queued and processed asynchronously.

**Monitoring results:**
- **Webhooks (recommended):** Subscribe to `batch_parse_run.processed` and `batch_parse_run.failed` events. The webhook payload indicates the batch has finished — fetch individual run results using `GET /parse_runs?batchId={id}`.
- **Polling:** Call `GET /batch_runs/{id}` to check the overall batch status, and use `GET /parse_runs?batchId={id}` to retrieve individual run results.

**Notes:**
- `inputs` must contain between 1 and 1,000 items.
- File input supports URLs, Extend file IDs, and raw text strings.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ParseRunsCreateBatchRequest{
        Inputs: []*extend.ParseRunsCreateBatchRequestInputsItem{
            &extend.ParseRunsCreateBatchRequestInputsItem{
                File: &extend.ParseRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/document1.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_abc123",
                },
            },
            &extend.ParseRunsCreateBatchRequestInputsItem{
                File: &extend.ParseRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/document2.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_def456",
                },
            },
            &extend.ParseRunsCreateBatchRequestInputsItem{
                File: &extend.ParseRunsCreateBatchRequestInputsItemFile{
                    FileFromText: &extend.FileFromText{
                        Text: "This is some raw text to parse.",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "source": "manual-entry",
                },
            },
        },
    }
client.ParseRuns.CreateBatch(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**inputs:** `[]*extend.ParseRunsCreateBatchRequestInputsItem` — An array of inputs to parse. Each item produces one parse run. Must contain between 1 and 1,000 items.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ParseConfig` — Optional parsing configuration applied to every run in this batch. If omitted, default parse settings are used.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*extend.RunPriority` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EditRuns
<details><summary><code>client.EditRuns.Create(request) -> *extend.EditRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Edit and manipulate PDF documents by detecting and filling form fields.

The Edit Runs endpoint allows you to convert and edit documents and get an edit run ID that can be used to check status and retrieve results with the Get Edit Run endpoint.

The request returns immediately with a `PROCESSING` status. Use webhooks or poll the Get Edit Run endpoint for results.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EditRunsCreateRequest{
        File: &extend.EditRunsCreateRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/form.pdf",
            },
        },
        Config: &extend.EditConfig{
            Instructions: extend.String(
                "Fill out the form with the provided data",
            ),
            AdvancedOptions: &extend.EditConfigAdvancedOptions{
                FlattenPdf: extend.Bool(
                    true,
                ),
            },
        },
    }
client.EditRuns.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `*extend.EditRunsCreateRequestFile` — The file to be edited. Files can be provided as a URL or an Extend file ID.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.EditConfig` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EditRuns.Retrieve(ID) -> *extend.EditRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve the status and results of an edit run.

Use this endpoint to get results for an edit run that has already completed, or to check on the status of an edit run initiated via the [Create Edit Run](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/edit/create-edit-run) endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EditRunsRetrieveRequest{}
client.EditRuns.Retrieve(
        context.TODO(),
        "edit_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier for the edit run.

Example: `"edr_xK9mLPqRtN3vS8wF5hB2cQ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EditRuns.Delete(ID) -> *extend.EditRunsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete an edit run and all associated data from Extend. This operation is permanent and cannot be undone.

This endpoint can be used if you'd like to manage data retention on your own rather than relying on automated data retention policies, or to make one-off deletions for your downstream customers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EditRunsDeleteRequest{}
client.EditRuns.Delete(
        context.TODO(),
        "edit_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the edit run to delete.

Example: `"edr_xK9mLPqRtN3vS8wF5hB2cQ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EditTemplates
<details><summary><code>client.EditTemplates.Retrieve(ID) -> *extend.EditTemplate</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a saved edit template by ID.

Use this endpoint to inspect the source file, default edit configuration, and optional schema generation configuration saved on an edit template. You can reuse the returned `config` with `POST /edit` or `POST /edit_runs`, and reuse `schemaConfig` with `POST /edit_schemas/generate`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EditTemplatesRetrieveRequest{}
client.EditTemplates.Retrieve(
        context.TODO(),
        "edit_template_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier for the edit template.

Example: `"edt_xK9mLPqRtN3vS8wF5hB2cQ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EditSchemas
<details><summary><code>client.EditSchemas.Generate(request) -> *extend.EditSchemaGenerationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Detect fields in a PDF form and synchronously return an edit schema payload.

Use this endpoint when you want Extend to bootstrap an `EditRootJSON` schema from an existing form, optionally mapping an existing schema onto the detected fields.

This endpoint returns the generated schema directly. There are no schema generation run resources to poll or delete.

For more details, see the [Generate Edit Schema guide](https://docs.extend.ai/2026-02-09/product/editing/generate-edit-schema) and the [Edit File guide](https://docs.extend.ai/2026-02-09/product/editing/edit).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EditSchemasGenerateRequest{
        File: &extend.EditSchemasGenerateRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/form.pdf",
            },
        },
        Config: &extend.EditSchemaGenerationConfig{
            Instructions: extend.String(
                "Detect the form fields and use human-readable field names.",
            ),
            AdvancedOptions: &extend.EditSchemaGenerationConfigAdvancedOptions{
                RadioEnumsEnabled: extend.Bool(
                    true,
                ),
            },
        },
    }
client.EditSchemas.Generate(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `*extend.EditSchemasGenerateRequestFile` — The file to analyze. Files can be provided as a URL or an Extend file ID.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.EditSchemaGenerationConfig` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ExtractRuns
<details><summary><code>client.ExtractRuns.List() -> *extend.ExtractRunsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all extract runs.

Returns a summary of each run. Use `GET /extract_runs/{id}` to retrieve the full object including `output` and `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractRunsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.ExtractRuns.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `*extend.ProcessorRunStatus` 
    
</dd>
</dl>

<dl>
<dd>

**extractorID:** `*string` 

Filters extract runs by the extractor ID. If not provided, all extract runs are returned.

Example: `"ex_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**batchID:** `*string` 

Filters runs by the batch they belong to. Only returns runs created as part of the specified batch.

Example: `"bpr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**sourceID:** `*extend.RunSourceID` — Filters runs by the source ID.
    
</dd>
</dl>

<dl>
<dd>

**source:** `*extend.RunSource` — Filters runs by the source that created them. If not provided, runs from all sources are returned.
    
</dd>
</dl>

<dl>
<dd>

**fileNameContains:** `*string` 

Filters runs by the name of the file. Only returns runs where the file name contains this string.

Example: `"invoice"`
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ExtractRuns.Create(request) -> *extend.ExtractRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Extract structured data from a file using an existing extractor or an inline configuration.

The request returns immediately with a `PROCESSING` status. Use webhooks or poll the Get Extract Run endpoint for results.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractRunsCreateRequest{
        Extractor: &extend.ExtractRunsCreateRequestExtractor{
            ID: "ex_1234567890",
        },
        File: &extend.ExtractRunsCreateRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/invoice.pdf",
            },
        },
    }
client.ExtractRuns.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extractor:** `*extend.ExtractRunsCreateRequestExtractor` — Reference to an existing extractor. One of `extractor` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ExtractConfigJSON` — Inline extract configuration. One of `extractor` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.ExtractRunsCreateRequestFile` — The file to be extracted from. Files can be provided as a URL, Extend file ID, or raw text.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*extend.RunPriority` 
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ExtractRuns.Retrieve(ID) -> *extend.ExtractRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve details about a specific extract run, including its status, outputs, and any edits made during review.

A common use case for this endpoint is to poll for the status and final output of an extract run when using the [Create Extract Run](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/extract/create-extract-run) endpoint. For instance, if you do not want to not configure webhooks to receive the output via completion/failure events.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractRunsRetrieveRequest{}
client.ExtractRuns.Retrieve(
        context.TODO(),
        "extract_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier for this extract run.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ExtractRuns.Delete(ID) -> *extend.ExtractRunsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete an extract run and all associated data from Extend. This operation is permanent and cannot be undone.

This endpoint can be used if you'd like to manage data retention on your own rather than automated data retention policies. Or make one-off deletions for your downstream customers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractRunsDeleteRequest{}
client.ExtractRuns.Delete(
        context.TODO(),
        "id",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the extract run.
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ExtractRuns.Cancel(ID) -> *extend.ExtractRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel an in-progress extract run.

Note: Only extract runs with a status of `"PROCESSING"` can be cancelled. Extractor runs that have already completed, failed, or been cancelled cannot be cancelled again.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractRunsCancelRequest{}
client.ExtractRuns.Cancel(
        context.TODO(),
        "extract_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the extract run to cancel.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ExtractRuns.CreateBatch(request) -> *extend.BatchRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit up to **1,000 files** for extraction in a single request. Each file is processed as an independent extract run using the same extractor and configuration.

Unlike the single [Extract File (Async)](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/extract/create-extract-run) endpoint, this batch endpoint accepts an `inputs` array and immediately returns a `BatchRun` object containing a batch `id` and a `PENDING` status. The individual runs are then queued and processed asynchronously.

**Monitoring results:**
- **Webhooks (recommended):** Subscribe to `batch_processor_run.processed` and `batch_processor_run.failed` events. The webhook payload indicates the batch has finished — fetch individual run results using `GET /extract_runs?batchId={id}`.
- **Polling:** Call `GET /batch_runs/{id}` to check the overall batch status, and use `GET /extract_runs` filtered by `batchId` to retrieve individual run results.

**Notes:**
- A processor reference (`extractor.id`) is required — inline `config` is not supported for batch requests.
- `inputs` must contain between 1 and 1,000 items.
- All inputs in a batch use the same extractor version and override config.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractRunsCreateBatchRequest{
        Extractor: &extend.ExtractRunsCreateBatchRequestExtractor{
            ID: "ex_xK9mLPqRtN3vS8wF5hB2cQ",
        },
        Inputs: []*extend.ExtractRunsCreateBatchRequestInputsItem{
            &extend.ExtractRunsCreateBatchRequestInputsItem{
                File: &extend.ExtractRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/invoice1.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_abc123",
                },
            },
            &extend.ExtractRunsCreateBatchRequestInputsItem{
                File: &extend.ExtractRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/invoice2.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_def456",
                },
            },
            &extend.ExtractRunsCreateBatchRequestInputsItem{
                File: &extend.ExtractRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/invoice3.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_ghi789",
                },
            },
        },
    }
client.ExtractRuns.CreateBatch(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extractor:** `*extend.ExtractRunsCreateBatchRequestExtractor` — Reference to the extractor to run against every input in this batch.
    
</dd>
</dl>

<dl>
<dd>

**inputs:** `[]*extend.ExtractRunsCreateBatchRequestInputsItem` — An array of inputs to process. Each item produces one extract run. Must contain between 1 and 1,000 items.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*extend.RunPriority` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Extractors
<details><summary><code>client.Extractors.List() -> *extend.ExtractorsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all extractors.

Returns a summary of each extractor. Use `GET /extractors/{id}` to retrieve the full object including `draftVersion`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractorsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.Extractors.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Extractors.Create(request) -> *extend.Extractor</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new extractor.

You can optionally provide a `generate` object to automatically generate an extraction schema from sample documents using AI. `generate` is mutually exclusive with `config` and `cloneExtractorId`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractorsCreateRequest{
        Name: "Invoice Extractor",
        Config: &extend.ExtractConfigJSON{
            Schema: map[string]any{
                "properties": map[string]any{
                    "invoice_number": map[string]any{
                        "description": "The invoice number",
                        "type": []any{
                            "string",
                            "null",
                        },
                    },
                    "total_amount": map[string]any{
                        "description": "The total amount due",
                        "type": []any{
                            "number",
                            "null",
                        },
                    },
                    "vendor_name": map[string]any{
                        "description": "The name of the vendor",
                        "type": []any{
                            "string",
                            "null",
                        },
                    },
                },
                "type": "object",
            },
        },
    }
client.Extractors.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `string` — The name of the extractor.
    
</dd>
</dl>

<dl>
<dd>

**cloneExtractorID:** `*string` 

The ID of an existing extractor to clone. If provided, the new extractor will be created with the same config as the extractor with this ID. Cannot be provided together with `config` or `generate`.

Example: `"ex_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ExtractConfigJSON` — The configuration for the extractor. Cannot be provided together with `cloneExtractorId` or `generate`.
    
</dd>
</dl>

<dl>
<dd>

**generate:** `*extend.ExtractorsCreateRequestGenerate` 

If provided, an extraction schema is automatically generated from the supplied sample documents and applied to the extractor's draft. The response includes the extractor with the generated schema already in place.

Cannot be provided together with `config` or `cloneExtractorId`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Extractors.Retrieve(ID) -> *extend.Extractor</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of an extractor.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractorsRetrieveRequest{}
client.Extractors.Retrieve(
        context.TODO(),
        "extractor_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the extractor to get.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Extractors.Update(ID, request) -> *extend.Extractor</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an existing extractor.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractorsUpdateRequest{
        Name: extend.String(
            "Invoice Extractor v2",
        ),
    }
client.Extractors.Update(
        context.TODO(),
        "extractor_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the extractor to update.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The new name of the extractor.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ExtractConfigJSON` — The new configuration for the extractor. This will update the draft version of the extractor.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ExtractorVersions
<details><summary><code>client.ExtractorVersions.List(ExtractorID) -> *extend.ExtractorVersionsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to fetch all versions of a given extractor, including the current `draft` version.

Versions are returned in descending order of creation (newest first) with the `draft` version first. The `draft` version is the latest unpublished version of the extractor, which can be published to create a new version. It might not have any changes from the last published version.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractorVersionsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.ExtractorVersions.List(
        context.TODO(),
        "extractor_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extractorID:** `string` 

The ID of the extractor.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ExtractorVersions.Create(ExtractorID, request) -> *extend.ExtractorVersion</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to publish a new version of an existing extractor. Publishing a new version creates a snapshot of the extractor's current configuration and makes it available for use in workflows.

Publishing a new version does not automatically update existing workflows using this extractor. You may need to manually update workflows to use the new version if desired.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractorVersionsCreateRequest{
        ReleaseType: extend.ReleaseTypeMinor,
        Description: extend.String(
            "Updated extraction rules for better accuracy",
        ),
    }
client.ExtractorVersions.Create(
        context.TODO(),
        "extractor_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extractorID:** `string` 

The ID of the extractor.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**releaseType:** `*extend.ReleaseType` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*extend.VersionDescription` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ExtractConfigJSON` — The configuration for this version of the extractor.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ExtractorVersions.Retrieve(ExtractorID, VersionID) -> *extend.ExtractorVersion</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a specific version of an extractor in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ExtractorVersionsRetrieveRequest{}
client.ExtractorVersions.Retrieve(
        context.TODO(),
        "extractor_id_here",
        "draft",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extractorID:** `string` 

The ID of the extractor.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**versionID:** `string` 

The version to retrieve. Accepts any of the following:

- `"draft"` — returns the current draft version
- `"latest"` — returns the latest published version (falls back to draft if none published)
- A version number (e.g. `"0.1"`, `"1.0"`) — returns that specific published version
- A version ID (e.g. `"extv_QYk6jgHA_8CsO8rVWhyNC"`) — returns that specific version by ID
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ClassifyRuns
<details><summary><code>client.ClassifyRuns.List() -> *extend.ClassifyRunsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all classify runs.

Returns a summary of each run. Use `GET /classify_runs/{id}` to retrieve the full object including `output` and `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifyRunsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.ClassifyRuns.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `*extend.ProcessorRunStatus` 
    
</dd>
</dl>

<dl>
<dd>

**classifierID:** `*string` 

Filters classify runs by the classifier ID. If not provided, all classify runs are returned.

Example: `"cl_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**batchID:** `*string` 

Filters runs by the batch they belong to. Only returns runs created as part of the specified batch.

Example: `"bpr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**sourceID:** `*extend.RunSourceID` — Filters runs by the source ID.
    
</dd>
</dl>

<dl>
<dd>

**source:** `*extend.RunSource` — Filters runs by the source that created them. If not provided, runs from all sources are returned.
    
</dd>
</dl>

<dl>
<dd>

**fileNameContains:** `*string` 

Filters runs by the name of the file. Only returns runs where the file name contains this string.

Example: `"invoice"`
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ClassifyRuns.Create(request) -> *extend.ClassifyRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Classify a document using an existing classifier or an inline configuration.

The request returns immediately with a `PROCESSING` status. Use webhooks or poll the Get Classify Run endpoint for results.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifyRunsCreateRequest{
        Classifier: &extend.ClassifyRunsCreateRequestClassifier{
            ID: "cl_1234567890",
        },
        File: &extend.ClassifyRunsCreateRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/document.pdf",
            },
        },
    }
client.ClassifyRuns.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classifier:** `*extend.ClassifyRunsCreateRequestClassifier` — Reference to an existing classifier. One of `classifier` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ClassifyConfig` — Inline classify configuration. One of `classifier` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.ClassifyRunsCreateRequestFile` — The file to be classified. Files can be provided as a URL, an Extend file ID, or raw text.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*extend.RunPriority` 
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ClassifyRuns.Retrieve(ID) -> *extend.ClassifyRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve details about a specific classify run, including its status and outputs.

A common use case for this endpoint is to poll for the status and final output of a classify run when using the [Create Classify Run](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/classify/create-classify-run) endpoint. For instance, if you do not want to not configure webhooks to receive the output via completion/failure events.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifyRunsRetrieveRequest{}
client.ClassifyRuns.Retrieve(
        context.TODO(),
        "classify_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier for this classify run.

Example: `"cl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ClassifyRuns.Delete(ID) -> *extend.ClassifyRunsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a classify run and all associated data from Extend. This operation is permanent and cannot be undone.

This endpoint can be used if you'd like to manage data retention on your own rather than automated data retention policies. Or make one-off deletions for your downstream customers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifyRunsDeleteRequest{}
client.ClassifyRuns.Delete(
        context.TODO(),
        "id",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the classify run.
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ClassifyRuns.Cancel(ID) -> *extend.ClassifyRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel an in-progress classify run.

Note: Only classify runs with a status of `"PROCESSING"` can be cancelled. Classifier runs that have already completed, failed, or been cancelled cannot be cancelled again.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifyRunsCancelRequest{}
client.ClassifyRuns.Cancel(
        context.TODO(),
        "classify_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the classify run to cancel.

Example: `"cl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ClassifyRuns.CreateBatch(request) -> *extend.BatchRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit up to **1,000 files** for classification in a single request. Each file is processed as an independent classify run using the same classifier and configuration.

Unlike the single [Classify File (Async)](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/classify/create-classify-run) endpoint, this batch endpoint accepts an `inputs` array and immediately returns a `BatchRun` object containing a batch `id` and a `PENDING` status. The individual runs are then queued and processed asynchronously.

**Monitoring results:**
- **Webhooks (recommended):** Subscribe to `batch_processor_run.processed` and `batch_processor_run.failed` events. The webhook payload indicates the batch has finished — fetch individual run results using `GET /classify_runs?batchId={id}`.
- **Polling:** Call `GET /batch_runs/{id}` to check the overall batch status, and use `GET /classify_runs` filtered by `batchId` to retrieve individual run results.

**Notes:**
- A processor reference (`classifier.id`) is required — inline `config` is not supported for batch requests.
- `inputs` must contain between 1 and 1,000 items.
- All inputs in a batch use the same classifier version and override config.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifyRunsCreateBatchRequest{
        Classifier: &extend.ClassifyRunsCreateBatchRequestClassifier{
            ID: "cl_xK9mLPqRtN3vS8wF5hB2cQ",
        },
        Inputs: []*extend.ClassifyRunsCreateBatchRequestInputsItem{
            &extend.ClassifyRunsCreateBatchRequestInputsItem{
                File: &extend.ClassifyRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/document1.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_abc123",
                },
            },
            &extend.ClassifyRunsCreateBatchRequestInputsItem{
                File: &extend.ClassifyRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/document2.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_def456",
                },
            },
            &extend.ClassifyRunsCreateBatchRequestInputsItem{
                File: &extend.ClassifyRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/document3.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_ghi789",
                },
            },
        },
    }
client.ClassifyRuns.CreateBatch(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classifier:** `*extend.ClassifyRunsCreateBatchRequestClassifier` — Reference to the classifier to run against every input in this batch.
    
</dd>
</dl>

<dl>
<dd>

**inputs:** `[]*extend.ClassifyRunsCreateBatchRequestInputsItem` — An array of inputs to process. Each item produces one classify run. Must contain between 1 and 1,000 items.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*extend.RunPriority` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Classifiers
<details><summary><code>client.Classifiers.List() -> *extend.ClassifiersListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all classifiers.

Returns a summary of each classifier. Use `GET /classifiers/{id}` to retrieve the full object including `draftVersion`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifiersListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.Classifiers.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Classifiers.Create(request) -> *extend.Classifier</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new classifier.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifiersCreateRequest{
        Name: "Document Classifier",
        Config: &extend.ClassifyConfig{
            Classifications: []*extend.Classification{
                &extend.Classification{
                    ID: "invoice",
                    Type: "invoice",
                    Description: "An invoice or bill for goods or services",
                },
                &extend.Classification{
                    ID: "receipt",
                    Type: "receipt",
                    Description: "A receipt confirming payment",
                },
                &extend.Classification{
                    ID: "other",
                    Type: "other",
                    Description: "Any other document type",
                },
            },
        },
    }
client.Classifiers.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `string` — The name of the classifier.
    
</dd>
</dl>

<dl>
<dd>

**cloneClassifierID:** `*string` 

The ID of an existing classifier to clone. If provided, the new classifier will be created with the same config as the classifier with this ID. Cannot be provided together with `config`.

Example: `"cl_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ClassifyConfig` — The configuration for the classifier. Cannot be provided together with `cloneClassifierId`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Classifiers.Retrieve(ID) -> *extend.Classifier</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of a classifier.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifiersRetrieveRequest{}
client.Classifiers.Retrieve(
        context.TODO(),
        "classifier_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the classifier to get.

Example: `"cl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Classifiers.Update(ID, request) -> *extend.Classifier</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an existing classifier.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifiersUpdateRequest{
        Name: extend.String(
            "Document Classifier v2",
        ),
    }
client.Classifiers.Update(
        context.TODO(),
        "classifier_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the classifier to update.

Example: `"cl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The new name of the classifier.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ClassifyConfig` — The new configuration for the classifier. This will update the draft version of the classifier.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ClassifierVersions
<details><summary><code>client.ClassifierVersions.List(ClassifierID) -> *extend.ClassifierVersionsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to fetch all versions of a given classifier, including the current `draft` version.

Versions are returned in descending order of creation (newest first) with the `draft` version first. The `draft` version is the latest unpublished version of the classifier, which can be published to create a new version. It might not have any changes from the last published version.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifierVersionsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.ClassifierVersions.List(
        context.TODO(),
        "classifier_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classifierID:** `string` 

The ID of the classifier.

Example: `"cl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ClassifierVersions.Create(ClassifierID, request) -> *extend.ClassifierVersion</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to publish a new version of an existing classifier. Publishing a new version creates a snapshot of the classifier's current configuration and makes it available for use in workflows.

Publishing a new version does not automatically update existing workflows using this classifier. You may need to manually update workflows to use the new version if desired.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifierVersionsCreateRequest{
        ReleaseType: extend.ReleaseTypeMinor,
        Description: extend.String(
            "Added new document classification type",
        ),
    }
client.ClassifierVersions.Create(
        context.TODO(),
        "classifier_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classifierID:** `string` 

The ID of the classifier.

Example: `"cl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**releaseType:** `*extend.ReleaseType` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*extend.VersionDescription` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ClassifyConfig` — The configuration for this version of the classifier.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ClassifierVersions.Retrieve(ClassifierID, VersionID) -> *extend.ClassifierVersion</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a specific version of a classifier in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ClassifierVersionsRetrieveRequest{}
client.ClassifierVersions.Retrieve(
        context.TODO(),
        "classifier_id_here",
        "draft",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classifierID:** `string` 

The ID of the classifier.

Example: `"cl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**versionID:** `string` 

The version to retrieve. Accepts any of the following:

- `"draft"` — returns the current draft version
- `"latest"` — returns the latest published version (falls back to draft if none published)
- A version number (e.g. `"0.1"`, `"1.0"`) — returns that specific published version
- A version ID (e.g. `"clsv_QYk6jgHA_8CsO8rVWhyNC"`) — returns that specific version by ID
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SplitRuns
<details><summary><code>client.SplitRuns.List() -> *extend.SplitRunsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all split runs.

Returns a summary of each run. Use `GET /split_runs/{id}` to retrieve the full object including `output` and `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitRunsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.SplitRuns.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `*extend.ProcessorRunStatus` 
    
</dd>
</dl>

<dl>
<dd>

**splitterID:** `*string` 

Filters split runs by the splitter ID. If not provided, all split runs are returned.

Example: `"spl_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**batchID:** `*string` 

Filters runs by the batch they belong to. Only returns runs created as part of the specified batch.

Example: `"bpr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**sourceID:** `*extend.RunSourceID` — Filters runs by the source ID.
    
</dd>
</dl>

<dl>
<dd>

**source:** `*extend.RunSource` — Filters runs by the source that created them. If not provided, runs from all sources are returned.
    
</dd>
</dl>

<dl>
<dd>

**fileNameContains:** `*string` 

Filters runs by the name of the file. Only returns runs where the file name contains this string.

Example: `"invoice"`
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SplitRuns.Create(request) -> *extend.SplitRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Split a document into multiple parts using an existing splitter or an inline configuration.

The request returns immediately with a `PROCESSING` status. Use webhooks or poll the Get Split Run endpoint for results.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitRunsCreateRequest{
        Splitter: &extend.SplitRunsCreateRequestSplitter{
            ID: "spl_1234567890",
        },
        File: &extend.SplitRunsCreateRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/multi-document.pdf",
            },
        },
    }
client.SplitRuns.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**splitter:** `*extend.SplitRunsCreateRequestSplitter` — Reference to an existing splitter. One of `splitter` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.SplitConfig` — Inline splitter configuration. One of `splitter` or `config` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.SplitRunsCreateRequestFile` — The file to be split. Files can be provided as a URL or an Extend file ID.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*extend.RunPriority` 
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SplitRuns.Retrieve(ID) -> *extend.SplitRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve details about a specific split run, including its status and outputs.

A common use case for this endpoint is to poll for the status and final output of a split run when using the [Create Split Run](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/split/create-split-run) endpoint. For instance, if you do not want to not configure webhooks to receive the output via completion/failure events.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitRunsRetrieveRequest{}
client.SplitRuns.Retrieve(
        context.TODO(),
        "split_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier for this split run.

Example: `"spl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SplitRuns.Delete(ID) -> *extend.SplitRunsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a split run and all associated data from Extend. This operation is permanent and cannot be undone.

This endpoint can be used if you'd like to manage data retention on your own rather than automated data retention policies. Or make one-off deletions for your downstream customers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitRunsDeleteRequest{}
client.SplitRuns.Delete(
        context.TODO(),
        "id",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the split run.
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SplitRuns.Cancel(ID) -> *extend.SplitRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel an in-progress split run.

Note: Only split runs with a status of `"PROCESSING"` can be cancelled. Splitter runs that have already completed, failed, or been cancelled cannot be cancelled again.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitRunsCancelRequest{}
client.SplitRuns.Cancel(
        context.TODO(),
        "split_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the split run to cancel.

Example: `"spl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SplitRuns.CreateBatch(request) -> *extend.BatchRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit up to **1,000 files** for splitting in a single request. Each file is processed as an independent split run using the same splitter and configuration.

Unlike the single [Split File (Async)](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/split/create-split-run) endpoint, this batch endpoint accepts an `inputs` array and immediately returns a `BatchRun` object containing a batch `id` and a `PENDING` status. The individual runs are then queued and processed asynchronously.

**Monitoring results:**
- **Webhooks (recommended):** Subscribe to `batch_processor_run.processed` and `batch_processor_run.failed` events. The webhook payload indicates the batch has finished — fetch individual run results using `GET /split_runs?batchId={id}`.
- **Polling:** Call `GET /batch_runs/{id}` to check the overall batch status, and use `GET /split_runs` filtered by `batchId` to retrieve individual run results.

**Notes:**
- A processor reference (`splitter.id`) is required — inline `config` is not supported for batch requests.
- `inputs` must contain between 1 and 1,000 items.
- All inputs in a batch use the same splitter version and override config.
- Raw text input (`FileFromText`) is not supported for split runs. Use a URL or file ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitRunsCreateBatchRequest{
        Splitter: &extend.SplitRunsCreateBatchRequestSplitter{
            ID: "spl_xK9mLPqRtN3vS8wF5hB2cQ",
        },
        Inputs: []*extend.SplitRunsCreateBatchRequestInputsItem{
            &extend.SplitRunsCreateBatchRequestInputsItem{
                File: &extend.SplitRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/multi-doc1.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_abc123",
                },
            },
            &extend.SplitRunsCreateBatchRequestInputsItem{
                File: &extend.SplitRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/multi-doc2.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_def456",
                },
            },
            &extend.SplitRunsCreateBatchRequestInputsItem{
                File: &extend.SplitRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/multi-doc3.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_ghi789",
                },
            },
        },
    }
client.SplitRuns.CreateBatch(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**splitter:** `*extend.SplitRunsCreateBatchRequestSplitter` — Reference to the splitter to run against every input in this batch.
    
</dd>
</dl>

<dl>
<dd>

**inputs:** `[]*extend.SplitRunsCreateBatchRequestInputsItem` — An array of inputs to process. Each item produces one split run. Must contain between 1 and 1,000 items. Raw text input is not supported — use a URL or file ID.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*extend.RunPriority` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Splitters
<details><summary><code>client.Splitters.List() -> *extend.SplittersListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all splitters.

Returns a summary of each splitter. Use `GET /splitters/{id}` to retrieve the full object including `draftVersion`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplittersListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.Splitters.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Splitters.Create(request) -> *extend.Splitter</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new splitter.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplittersCreateRequest{
        Name: "Document Splitter",
        Config: &extend.SplitConfig{
            SplitClassifications: []*extend.SplitClassification{
                &extend.SplitClassification{
                    ID: "invoice",
                    Type: "invoice",
                    Description: "An invoice or bill for goods or services",
                    IdentifierKey: extend.String(
                        "invoice number from the document header",
                    ),
                },
                &extend.SplitClassification{
                    ID: "receipt",
                    Type: "receipt",
                    Description: "A receipt confirming payment",
                    IdentifierKey: extend.String(
                        "receipt number",
                    ),
                },
                &extend.SplitClassification{
                    ID: "other",
                    Type: "other",
                    Description: "Any other document type",
                },
            },
        },
    }
client.Splitters.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `string` — The name of the splitter.
    
</dd>
</dl>

<dl>
<dd>

**cloneSplitterID:** `*string` 

The ID of an existing splitter to clone. If provided, the new splitter will be created with the same config as the splitter with this ID. Cannot be provided together with `config`.

Example: `"spl_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.SplitConfig` — The configuration for the splitter. Cannot be provided together with `cloneSplitterId`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Splitters.Retrieve(ID) -> *extend.Splitter</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of a splitter.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplittersRetrieveRequest{}
client.Splitters.Retrieve(
        context.TODO(),
        "splitter_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the splitter to get.

Example: `"spl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Splitters.Update(ID, request) -> *extend.Splitter</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an existing splitter.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplittersUpdateRequest{
        Name: extend.String(
            "Document Splitter v2",
        ),
    }
client.Splitters.Update(
        context.TODO(),
        "splitter_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the splitter to update.

Example: `"spl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The new name of the splitter.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.SplitConfig` — The new configuration for the splitter. This will update the draft version of the splitter.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SplitterVersions
<details><summary><code>client.SplitterVersions.List(SplitterID) -> *extend.SplitterVersionsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to fetch all versions of a given splitter, including the current `draft` version.

Versions are returned in descending order of creation (newest first) with the `draft` version first. The `draft` version is the latest unpublished version of the splitter, which can be published to create a new version. It might not have any changes from the last published version.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitterVersionsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.SplitterVersions.List(
        context.TODO(),
        "splitter_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**splitterID:** `string` 

The ID of the splitter.

Example: `"spl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SplitterVersions.Create(SplitterID, request) -> *extend.SplitterVersion</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to publish a new version of an existing splitter. Publishing a new version creates a snapshot of the splitter's current configuration and makes it available for use in workflows.

Publishing a new version does not automatically update existing workflows using this splitter. You may need to manually update workflows to use the new version if desired.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitterVersionsCreateRequest{
        ReleaseType: extend.ReleaseTypeMinor,
        Description: extend.String(
            "Improved split boundary detection",
        ),
    }
client.SplitterVersions.Create(
        context.TODO(),
        "splitter_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**splitterID:** `string` 

The ID of the splitter.

Example: `"spl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**releaseType:** `*extend.ReleaseType` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*extend.VersionDescription` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.SplitConfig` — The configuration for this version of the splitter.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SplitterVersions.Retrieve(SplitterID, VersionID) -> *extend.SplitterVersion</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a specific version of a splitter in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.SplitterVersionsRetrieveRequest{}
client.SplitterVersions.Retrieve(
        context.TODO(),
        "splitter_id_here",
        "draft",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**splitterID:** `string` 

The ID of the splitter.

Example: `"spl_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**versionID:** `string` 

The version to retrieve. Accepts any of the following:

- `"draft"` — returns the current draft version
- `"latest"` — returns the latest published version (falls back to draft if none published)
- A version number (e.g. `"0.1"`, `"1.0"`) — returns that specific published version
- A version ID (e.g. `"splv_QYk6jgHA_8CsO8rVWhyNC"`) — returns that specific version by ID
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Workflows
<details><summary><code>client.Workflows.List() -> *extend.WorkflowsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all workflows. Returns a paginated list of workflow summaries.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.Workflows.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Workflows.Create(request) -> *extend.Workflow</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new workflow. Optionally provide `steps` to define the workflow's step graph.

When `steps` is omitted, the workflow is created with default steps (`TRIGGER` → `PARSE`). When `steps` is provided, the step graph is validated and the draft version is populated with the given steps.

**Note:** The default steps may change in the future. If your integration depends on a specific step graph, provide `steps` explicitly.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowsCreateRequest{
        Name: "Invoice Processing",
    }
client.Workflows.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `string` — The name of the workflow.
    
</dd>
</dl>

<dl>
<dd>

**steps:** `[]*extend.WorkflowStepDefinition` 

The steps that define the workflow's processing graph. Each step has a `type`, a unique `name`, and optional `next` entries that define routing to downstream steps.

When omitted, the workflow is created with default steps (`TRIGGER` → `PARSE`). The default steps may change in the future.

See the [Configuring Workflows via API guide](https://docs.extend.ai/2026-02-09/product/workflows/configuring-workflows-via-api) for step definitions, branching patterns, and examples.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Workflows.Retrieve(ID) -> *extend.Workflow</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of a workflow, including its draft version and steps.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Workflows.Retrieve(
        context.TODO(),
        "workflow_abc123",
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the workflow.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Workflows.Update(ID, request) -> *extend.Workflow</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update a workflow's draft. You can update the name, the steps, or both.

When `steps` is provided, the draft version's steps are replaced with the new set. Steps with matching names from the previous draft preserve their internal identity.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowsUpdateRequest{
        Name: extend.String(
            "Updated Invoice Processing",
        ),
    }
client.Workflows.Update(
        context.TODO(),
        "workflow_abc123",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the workflow to update.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The new name for the workflow.
    
</dd>
</dl>

<dl>
<dd>

**steps:** `[]*extend.WorkflowStepDefinition` 

The new step definitions for the draft version. Replaces all existing draft steps.

See the [Configuring Workflows via API guide](https://docs.extend.ai/2026-02-09/product/workflows/configuring-workflows-via-api) for step definitions, branching patterns, and examples.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## WorkflowVersions
<details><summary><code>client.WorkflowVersions.List(ID) -> *extend.WorkflowVersionsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all versions of a workflow, including the draft version. Returns a paginated list of version summaries.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowVersionsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.WorkflowVersions.List(
        context.TODO(),
        "workflow_abc123",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the workflow.
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WorkflowVersions.Create(ID, request) -> *extend.WorkflowVersion</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deploy a new version of a workflow. The deployed version becomes available for running workflow runs.

When `steps` is omitted, the current draft is deployed as-is. When `steps` is provided, the given steps are deployed directly without modifying the draft.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowVersionsCreateRequest{}
client.WorkflowVersions.Create(
        context.TODO(),
        "workflow_abc123",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the workflow to deploy.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — An optional name for this deployed version.
    
</dd>
</dl>

<dl>
<dd>

**steps:** `[]*extend.WorkflowStepDefinition` 

Optional step definitions. When provided, these steps are deployed directly without modifying the draft. When omitted, the current draft is deployed.

All configurable steps (`EXTRACT`, `CLASSIFY`, `SPLIT`, `CONDITIONAL_EXTRACT`, `RULE_VALIDATION`, `EXTERNAL_DATA_VALIDATION`) must include `config` when deploying. Unconfigured steps are rejected with a 400.

See the [Configuring Workflows via API guide](https://docs.extend.ai/2026-02-09/product/workflows/configuring-workflows-via-api) for step definitions, branching patterns, and examples.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WorkflowVersions.Retrieve(ID, VersionID) -> *extend.WorkflowVersion</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a specific version of a workflow, including its step definitions.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.WorkflowVersions.Retrieve(
        context.TODO(),
        "workflow_abc123",
        "draft",
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the workflow.
    
</dd>
</dl>

<dl>
<dd>

**versionID:** `string` 

The version to retrieve. Accepts any of the following:

- `"draft"` — returns the current draft version
- `"latest"` — returns the latest published version (falls back to draft if none published)
- A version number (e.g. `"1"`, `"2"`) — returns that specific published version
- A version ID (e.g. `"workflow_version_abc123"`) — returns that specific version by ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## WorkflowRuns
<details><summary><code>client.WorkflowRuns.List() -> *extend.WorkflowRunsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List runs of a Workflow. Workflows are sequences of steps that process files and data in a specific order to achieve a desired outcome. A WorkflowRun represents a single execution of a workflow against a file.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowRunsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.WorkflowRuns.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `*extend.WorkflowRunStatus` 
    
</dd>
</dl>

<dl>
<dd>

**workflowID:** `*string` 

Filters workflow runs by the workflow ID. If not provided, runs for all workflows are returned.

Example: `"workflow_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**batchID:** `*string` 

Filters workflow runs by the batch ID. This is useful for fetching all runs for a given batch created via the [Batch Run Workflow](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/workflow/batch-create-workflow-runs) endpoint.

Example: `"batch_7Ws31-F5"`
    
</dd>
</dl>

<dl>
<dd>

**fileNameContains:** `*string` 

Filters runs by the name of the file. Only returns runs where the file name contains this string.

Example: `"invoice"`
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WorkflowRuns.Create(request) -> *extend.WorkflowRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Run a workflow with a file. A workflow is a sequence of steps that process files and data in a specific order to achieve a desired outcome.

The request returns immediately with a `PROCESSING` status. Use webhooks or poll the Get Workflow Run endpoint for results.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowRunsCreateRequest{
        Workflow: &extend.WorkflowReference{
            ID: "wf_1234567890",
        },
        File: &extend.WorkflowRunsCreateRequestFile{
            FileFromURL: &extend.FileFromURL{
                URL: "https://example.com/invoice.pdf",
            },
        },
    }
client.WorkflowRuns.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**workflow:** `*extend.WorkflowReference` 
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.WorkflowRunsCreateRequestFile` — The file to be processed. Supported file types can be found [here](https://docs.extend.ai/2026-02-09/product/general/supported-file-types). Files can be provided as a URL, an Extend file ID, or raw text. If you wish to process more at a time, consider using the [Batch Run Workflow](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/workflow/batch-create-workflow-runs) endpoint.
    
</dd>
</dl>

<dl>
<dd>

**outputs:** `[]*extend.WorkflowRunsCreateRequestOutputsItem` — Predetermined outputs to be used for the workflow run. Generally not recommended for most use cases, however, can be useful in cases of overriding a classification in a workflow, or a subset of extraction fields when data is known.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*extend.RunPriority` 
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.RunMetadata` 
    
</dd>
</dl>

<dl>
<dd>

**secrets:** `*extend.RunSecrets` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WorkflowRuns.Retrieve(ID) -> *extend.WorkflowRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Once a workflow has been run, you can check the status and output of a specific WorkflowRun.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowRunsRetrieveRequest{}
client.WorkflowRuns.Retrieve(
        context.TODO(),
        "workflow_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the workflow run.

Example: `"workflow_run_xKm9pNv3qWsY_jL2tR5Dh"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WorkflowRuns.Update(ID, request) -> *extend.WorkflowRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

You can update the name and metadata of an in progress WorkflowRun at any time using this endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowRunsUpdateRequest{
        Name: extend.String(
            "Invoice #12345",
        ),
        Metadata: map[string]any{
            "customerId": "cust_abc123",
            "source": "email-inbox",
        },
    }
client.WorkflowRuns.Update(
        context.TODO(),
        "workflow_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the workflow run.

Example: `"workflow_run_xKm9pNv3qWsY_jL2tR5Dh"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — An optional name that can be assigned to a specific WorkflowRun
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `map[string]any` 

A metadata object that can be assigned to a specific WorkflowRun. If metadata already exists on this WorkflowRun, the newly incoming metadata will be merged with the existing metadata, with the incoming metadata taking field precedence.

You can include any arbitrary `key : value` pairs in this object.

To categorize workflow runs for billing and usage tracking, include `extend:usage_tags` with an array of string values (e.g., `{"extend:usage_tags": ["production", "team-eng", "customer-123"]}`). Tags must contain only alphanumeric characters, hyphens, and underscores; any special characters will be automatically removed.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WorkflowRuns.Delete(ID) -> *extend.WorkflowRunsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a workflow run and all associated data from Extend. This operation is permanent and cannot be undone.

This endpoint can be used if you'd like to manage data retention on your own rather than automated data retention policies. Or make one-off deletions for your downstream customers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowRunsDeleteRequest{}
client.WorkflowRuns.Delete(
        context.TODO(),
        "workflow_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the workflow run.

Example: `"workflow_run_xKm9pNv3qWsY_jL2tR5Dh"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WorkflowRuns.Cancel(ID) -> *extend.WorkflowRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a running workflow run by its ID. This endpoint allows you to stop a workflow run that is currently in progress.

Note: Only workflow runs with a status of `PROCESSING` or `PENDING` can be cancelled. Workflow runs that are completed, failed, in review, rejected, or already cancelled cannot be cancelled.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowRunsCancelRequest{}
client.WorkflowRuns.Cancel(
        context.TODO(),
        "workflow_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the workflow run.

Example: `"workflow_run_xKm9pNv3qWsY_jL2tR5Dh"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WorkflowRuns.CreateBatch(request) -> *extend.WorkflowRunsCreateBatchResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to efficiently initiate large batches of workflow runs in a single request (up to 1,000 in a single request, but you can queue up multiple batches in rapid succession). It accepts an array of inputs, each containing a file and metadata pair. The primary use case for this endpoint is for doing large bulk runs of >1000 files at a time that can process over the course of a few hours without needing to manage rate limits that would likely occur using the primary run endpoint.

Unlike the single [Run Workflow](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/workflow/create-workflow-run) endpoint which returns the details of the created workflow runs immediately, this batch endpoint returns a `batchId`.

Our recommended usage pattern is to integrate with [Webhooks](https://docs.extend.ai/2026-02-09/product/webhooks/configuration) for consuming results, using the `metadata` and `batchId` to match up results to the original inputs in your downstream systems. However, you can integrate in a polling mechanism by using a combination of the [List Workflow Runs](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/workflow/list-workflow-runs) endpoint to fetch all runs via a batch, and then [Get Workflow Run](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/workflow/get-workflow-run) to fetch the full outputs each run.

**Priority:** All workflow runs created through this batch endpoint are automatically assigned a priority of 90.

**Processing and Monitoring:**
Upon successful submission, the endpoint returns a `batchId`. The individual workflow runs are then queued for processing.

- **Monitoring:** Track the progress and consume results of individual runs using [Webhooks](https://docs.extend.ai/2026-02-09/product/webhooks/configuration). Subscribe to events like `workflow_run.completed`, `workflow_run.failed`, etc. The webhook payload for these events will include the corresponding `batchId` and the `metadata` you provided for each input.
- **Fetching Results:** You can also use the [List Workflow Runs](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/workflow/list-workflow-runs) endpoint and filter using the `batchId` query param.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WorkflowRunsCreateBatchRequest{
        Workflow: &extend.WorkflowReference{
            ID: "wf_1234567890",
        },
        Inputs: []*extend.WorkflowRunsCreateBatchRequestInputsItem{
            &extend.WorkflowRunsCreateBatchRequestInputsItem{
                File: &extend.WorkflowRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/invoice1.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_abc123",
                },
            },
            &extend.WorkflowRunsCreateBatchRequestInputsItem{
                File: &extend.WorkflowRunsCreateBatchRequestInputsItemFile{
                    FileFromURL: &extend.FileFromURL{
                        URL: "https://example.com/invoice2.pdf",
                    },
                },
                Metadata: &extend.RunMetadata{
                    "customerId": "cust_def456",
                },
            },
        },
    }
client.WorkflowRuns.CreateBatch(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**workflow:** `*extend.WorkflowReference` 
    
</dd>
</dl>

<dl>
<dd>

**inputs:** `[]*extend.WorkflowRunsCreateBatchRequestInputsItem` — An array of input objects to be processed by the workflow. Each object represents a single workflow run to be created. The array must contain at least 1 input and at most 1000 inputs.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ProcessorRun
<details><summary><code>client.ProcessorRun.List() -> *extend.ProcessorRunListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List runs of a Processor. A ProcessorRun represents a single execution of a processor against a file.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorRunListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.ProcessorRun.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `*extend.LegacyProcessorStatus` 

Filters processor runs by their status. If not provided, no filter is applied.

 The status of a processor run:
 * `"PENDING"` - The processor run has not started yet
 * `"PROCESSING"` - The processor run is in progress
 * `"PROCESSED"` - The processor run completed successfully
 * `"FAILED"` - The processor run encountered an error
 * `"CANCELLED"` - The processor run was cancelled
    
</dd>
</dl>

<dl>
<dd>

**processorID:** `*string` 

Filters processor runs by the processor ID. If not provided, runs for all processors are returned.

Example: `"ex_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**processorType:** `*extend.LegacyProcessorType` 

Filters processor runs by the processor type. If not provided, runs for all processor types are returned.

Example: `"EXTRACT"`
    
</dd>
</dl>

<dl>
<dd>

**sourceID:** `*string` 

Filters processor runs by the source ID. The source ID corresponds to the entity that created the processor run.

Example: `"workflow_run_123"`
    
</dd>
</dl>

<dl>
<dd>

**source:** `*extend.ProcessorRunListRequestSource` 

Filters processor runs by the source that created them. If not provided, runs from all sources are returned.

The source of the processor run:
* `"ADMIN"` - Created by admin
* `"BATCH_PROCESSOR_RUN"` - Created from a batch processor run
* `"PLAYGROUND"` - Created from playground
* `"WORKFLOW_CONFIGURATION"` - Created from workflow configuration
* `"WORKFLOW_RUN"` - Created from a workflow run
* `"STUDIO"` - Created from Studio
* `"API"` - Created via API
    
</dd>
</dl>

<dl>
<dd>

**fileNameContains:** `*string` 

Filters processor runs by the name of the file. Only returns processor runs where the file name contains this string.

Example: `"invoice"`
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.LegacySortByEnum` — Sorts the processor runs by the given field.
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.LegacySortDirEnum` — Sorts the processor runs in ascending or descending order. Ascending order means the earliest processor run is returned first.
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.LegacyNextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.LegacyMaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ProcessorRun.Create(request) -> *extend.ProcessorRunCreateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Run processors (extraction, classification, splitting, etc.) on a given document.

**Synchronous vs Asynchronous Processing:**
- **Asynchronous (default)**: Returns immediately with `PROCESSING` status. Use webhooks or polling to get results.
- **Synchronous**: Set `sync: true` to wait for completion and get final results in the response (5-minute timeout).

**For asynchronous processing:**
- You can [configure webhooks](https://docs.extend.ai/2026-02-09/product/webhooks/configuration) to receive notifications when a processor run is complete or failed.
- Or you can [poll the get endpoint](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/legacy/get-processor-run) for updates on the status of the processor run.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorRunCreateRequest{
        ProcessorID: "processor_id_here",
    }
client.ProcessorRun.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**processorID:** `extend.LegacyProcessorID` 
    
</dd>
</dl>

<dl>
<dd>

**version:** `*string` 

An optional version of the processor to use. When not supplied, the most recent published version of the processor will be used. Special values include:
- `"latest"` for the most recent published version. If there are no published versions, the draft version will be used.
- `"draft"` for the draft version.
- Specific version numbers corresponding to versions your team has published, e.g. `"1.0"`, `"2.2"`, etc.
    
</dd>
</dl>

<dl>
<dd>

**file:** `*extend.LegacyProcessorRunFileInput` — The file to be processed. One of `file` or `rawText` must be provided. Supported file types can be found [here](https://docs.extend.ai/2026-02-09/product/general/supported-file-types).
    
</dd>
</dl>

<dl>
<dd>

**rawText:** `*string` — A raw string to be processed. Can be used in place of file when passing raw text data streams. One of `file` or `rawText` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**sync:** `*bool` 

Whether to run the processor synchronously. When `true`, the request will wait for the processor run to complete and return the final results. When `false` (default), the request returns immediately with a `PROCESSING` status, and you can poll for completion or use webhooks. For production use cases, we recommending leaving sync off and building around an async integration for more resiliency, unless your use case is predictably fast (e.g. sub < 30 seconds) run time or otherwise have integration constraints that require a synchronous API. See [Async Processing](https://docs.extend.ai/2026-02-09/developers/async-processing) for more details.

**Timeout**: Synchronous requests have a 5-minute timeout. If the processor run takes longer, it will continue processing asynchronously and you can retrieve the results via the GET endpoint.
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*int` — An optional value used to determine the relative order of ProcessorRuns when rate limiting is in effect. Lower values will be prioritized before higher values.
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `*extend.LegacyJSONObject` 

An optional object that can be passed in to identify the run of the document processor. It will be returned back to you in the response and webhooks.

To categorize processor runs for billing and usage tracking, include `extend:usage_tags` with an array of string values (e.g., `{"extend:usage_tags": ["production", "team-eng", "customer-123"]}`). Tags must contain only alphanumeric characters, hyphens, and underscores; any special characters will be automatically removed.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ProcessorRunCreateRequestConfig` — The configuration for the processor run. If this is provided, this config will be used. If not provided, the config for the specific version you provide will be used. The type of configuration must match the processor type.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ProcessorRun.Get(ID) -> *extend.ProcessorRunGetResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve details about a specific processor run, including its status, outputs, and any edits made during review.

A common use case for this endpoint is to poll for the status and final output of an async processor run when using the [Run Processor](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/legacy/create-processor-run) endpoint. For instance, if you do not want to not configure webhooks to receive the output via completion/failure events.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorRunGetRequest{}
client.ProcessorRun.Get(
        context.TODO(),
        "processor_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier for this processor run.

Example: `"exr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ProcessorRun.Delete(ID) -> *extend.ProcessorRunDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a processor run and all associated data from Extend. This operation is permanent and cannot be undone.

This endpoint can be used if you'd like to manage data retention on your own rather than automated data retention policies. Or make one-off deletions for your downstream customers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorRunDeleteRequest{}
client.ProcessorRun.Delete(
        context.TODO(),
        "processor_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the processor run to delete.

Example: `"exr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ProcessorRun.Cancel(ID) -> *extend.ProcessorRunCancelResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a running processor run by its ID. This endpoint allows you to stop a processor run that is currently in progress.

Note: Only processor runs with a status of `"PROCESSING"` can be cancelled. Processor runs that have already completed, failed, or been cancelled cannot be cancelled again.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorRunCancelRequest{}
client.ProcessorRun.Cancel(
        context.TODO(),
        "processor_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier for the processor run to cancel.

Example: `"exr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Processor
<details><summary><code>client.Processor.List() -> *extend.LegacyListProcessorsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all processors in your organization
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorListRequest{}
client.Processor.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `*extend.LegacyProcessorType` — Filter processors by type
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*string` — Token for retrieving the next page of results
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*int` — Maximum number of processors to return per page
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.ProcessorListRequestSortBy` — Field to sort by
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.ProcessorListRequestSortDir` — Sort direction
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Processor.Create(request) -> *extend.ProcessorCreateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new processor in Extend, optionally cloning from an existing processor
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorCreateRequest{
        Name: "My Processor Name",
        Type: extend.LegacyProcessorTypeExtract,
    }
client.Processor.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `string` — The name of the new processor
    
</dd>
</dl>

<dl>
<dd>

**type_:** `*extend.LegacyProcessorType` 
    
</dd>
</dl>

<dl>
<dd>

**cloneProcessorID:** `*string` 

The ID of an existing processor to clone. One of `cloneProcessorId` or `config` must be provided.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ProcessorCreateRequestConfig` — The configuration for the processor. The type of configuration must match the processor type. One of `cloneProcessorId` or `config` must be provided.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Processor.Update(ID, request) -> *extend.ProcessorUpdateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an existing processor in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorUpdateRequest{}
client.Processor.Update(
        context.TODO(),
        "processor_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the processor to update.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The new name for the processor
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ProcessorUpdateRequestConfig` 

The new configuration for the processor. The type of configuration must match the processor type:
* For classification processors, use `ClassificationConfig`
* For extraction processors, use `ExtractionConfig`
* For splitter processors, use `SplitterConfig`
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ProcessorVersion
<details><summary><code>client.ProcessorVersion.List(ID) -> *extend.ProcessorVersionListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to fetch all versions of a given processor, including the current `draft` version.

Versions are typically returned in descending order of creation (newest first), but this should be confirmed in the actual implementation.
The `draft` version is the latest unpublished version of the processor, which can be published to create a new version. It might not have any changes from the last published version.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorVersionListRequest{}
client.ProcessorVersion.List(
        context.TODO(),
        "processor_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the processor to retrieve versions for.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ProcessorVersion.Create(ID, request) -> *extend.ProcessorVersionCreateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

This endpoint allows you to publish a new version of an existing processor. Publishing a new version creates a snapshot of the processor's current configuration and makes it available for use in workflows.

Publishing a new version does not automatically update existing workflows using this processor. You may need to manually update workflows to use the new version if desired.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorVersionCreateRequest{
        ReleaseType: extend.ProcessorVersionCreateRequestReleaseTypeMajor,
    }
client.ProcessorVersion.Create(
        context.TODO(),
        "processor_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the processor to publish a new version for.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**releaseType:** `*extend.ProcessorVersionCreateRequestReleaseType` — The type of release for this version. The two options are "major" and "minor", which will increment the version number accordingly.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — A description of the changes in this version. This helps track the evolution of the processor over time.
    
</dd>
</dl>

<dl>
<dd>

**config:** `*extend.ProcessorVersionCreateRequestConfig` — The configuration for this version of the processor. The type of configuration must match the processor type.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ProcessorVersion.Get(ProcessorID, ProcessorVersionID) -> *extend.ProcessorVersionGetResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a specific version of a processor in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.ProcessorVersionGetRequest{}
client.ProcessorVersion.Get(
        context.TODO(),
        "processor_id_here",
        "processor_version_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**processorID:** `string` 

The ID of the processor.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**processorVersionID:** `string` 

The ID of the specific processor version to retrieve.

Example: `"exv_QYk6jgHA_8CsO8rVWhyNC"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## BatchProcessorRun
<details><summary><code>client.BatchProcessorRun.Get(ID) -> *extend.BatchProcessorRunGetResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve details about a batch processor run, including evaluation runs.

**Deprecated:** This endpoint is maintained for backwards compatibility only and will be replaced in a future API version. Use [Get Evaluation Set Run](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/evaluation/get-evaluation-set-run) for interacting with evaluation set runs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.BatchProcessorRunGetRequest{}
client.BatchProcessorRun.Get(
        context.TODO(),
        "bpr_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier of the batch processor run to retrieve.

Example: `"bpr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## BatchRuns
<details><summary><code>client.BatchRuns.Get(ID) -> *extend.BatchRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve the status of a batch run by its ID. The `status` field reflects the aggregate state of the batch.

This is a unified endpoint that works for batches created via any of the batch submission endpoints (`POST /parse_runs/batch`, `POST /extract_runs/batch`, `POST /classify_runs/batch`, `POST /split_runs/batch`).

| Status | Meaning |
|---|---|
| `PENDING` | Queued, not yet started |
| `PROCESSING` | Runs are actively being processed |
| `PROCESSED` | All runs have completed |
| `FAILED` | The batch encountered a fatal error |
| `CANCELLED` | The batch was cancelled |

To retrieve individual run results, use the List endpoint for the relevant type filtered by `batchId`:
- `GET /parse_runs?batchId={id}`
- `GET /extract_runs?batchId={id}`
- `GET /classify_runs?batchId={id}`
- `GET /split_runs?batchId={id}`
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.BatchRuns.Get(
        context.TODO(),
        "bpr_Xj8mK2pL9nR4vT7qY5wZ",
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The unique identifier of the batch processor run to retrieve.

Example: `"bpr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EvaluationSets
<details><summary><code>client.EvaluationSets.List() -> *extend.EvaluationSetsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List evaluation sets in your account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetsListRequest{
        EntityID: extend.String(
            "entity_id_here",
        ),
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.EvaluationSets.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**entityID:** `*string` 

The ID of the extractor, classifier, or splitter to filter evaluation sets by.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EvaluationSets.Create(request) -> *extend.EvaluationSet</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Evaluation sets are collections of files and expected outputs that are used to evaluate the performance of a given extractor, classifier, or splitter. This endpoint will create a new evaluation set, which items can be added to using the [Create Evaluation Set Item](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/evaluation/create-evaluation-set-item) endpoint.

Note: It is not necessary to create an evaluation set via API. You can also create an evaluation set via the Extend dashboard and take the ID from there. To learn more about how to create evaluation sets, see the [Evaluation Sets](https://docs.extend.ai/2026-02-09/product/evaluation/overview) product page.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetsCreateRequest{
        Name: "Invoice Processing Test Set",
        Description: extend.String(
            "Q4 vendor invoices for accuracy testing",
        ),
        EntityID: "ex_1234567890",
    }
client.EvaluationSets.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `string` 

The name of the evaluation set.

Example: `"Invoice Processing Test Set"`
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 

A description of what this evaluation set is used for.

Example: `"Q4 2023 vendor invoices"`
    
</dd>
</dl>

<dl>
<dd>

**entityID:** `string` 

The ID of the extractor, classifier, or splitter to create an evaluation set for. Evaluation sets can in theory be run against any extractor, classifier, or splitter, but it is required to associate the evaluation set with a primary extractor, classifier, or splitter.

Example: `"ex_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EvaluationSets.Retrieve(ID) -> *extend.EvaluationSet</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a specific evaluation set by ID. This returns an evaluation set object, but does not include the items in the evaluation set. You can use the [List Evaluation Set Items](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/evaluation/list-evaluation-set-items) endpoint to get the items in an evaluation set.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetsRetrieveRequest{}
client.EvaluationSets.Retrieve(
        context.TODO(),
        "evaluation_set_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the evaluation set.

Example: `"ev_2LcgeY_mp2T5yPaEuq5Lw"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EvaluationSetItems
<details><summary><code>client.EvaluationSetItems.List(EvaluationSetID) -> *extend.EvaluationSetItemsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List items in a specific evaluation set.

Returns a summary of each evaluation set item. Use the [Get Evaluation Set Item](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/evaluation/get-evaluation-set-item) endpoint to get the full details of an evaluation set item.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetItemsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.EvaluationSetItems.List(
        context.TODO(),
        "evaluation_set_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**evaluationSetID:** `string` 

The ID of the evaluation set.

Example: `"ev_2LcgeY_mp2T5yPaEuq5Lw"`
    
</dd>
</dl>

<dl>
<dd>

**sortBy:** `*extend.SortBy` 
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EvaluationSetItems.Create(EvaluationSetID, request) -> *extend.EvaluationSetItemsCreateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Evaluation set items are the individual files and expected outputs that are used to evaluate the performance of a given extractor, classifier, or splitter in Extend. This endpoint will create new evaluation set items in Extend, which will be used during an evaluation run.

**Limit:** You can create up to 100 items at a time.

Learn more about how to create evaluation set items in the [Evaluation Sets](https://docs.extend.ai/2026-02-09/product/evaluation/overview) product page.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetItemsCreateRequest{
        Items: []*extend.EvaluationSetItemsCreateRequestItemsItem{
            &extend.EvaluationSetItemsCreateRequestItemsItem{
                FileID: "file_xK9mLPqRtN3vS8wF5hB2cQ",
                ExpectedOutput: &extend.ProvidedProcessorOutput{
                    ProvidedExtractOutput: &extend.ProvidedExtractOutput{
                        Value: &extend.JSONObject{
                            "invoice_number": "INV-001",
                            "total_amount": 1500,
                            "vendor_name": "Acme Corp",
                        },
                    },
                },
            },
        },
    }
client.EvaluationSetItems.Create(
        context.TODO(),
        "evaluation_set_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**evaluationSetID:** `string` 

The ID of the evaluation set.

Example: `"ev_2LcgeY_mp2T5yPaEuq5Lw"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**items:** `[]*extend.EvaluationSetItemsCreateRequestItemsItem` — An array of objects representing the evaluation set items to create.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EvaluationSetItems.Retrieve(EvaluationSetID, ItemID) -> *extend.EvaluationSetItem</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of an evaluation set item.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetItemsRetrieveRequest{}
client.EvaluationSetItems.Retrieve(
        context.TODO(),
        "evaluation_set_id_here",
        "evaluation_set_item_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**evaluationSetID:** `string` 

The ID of the evaluation set.

Example: `"ev_2LcgeY_mp2T5yPaEuq5Lw"`
    
</dd>
</dl>

<dl>
<dd>

**itemID:** `string` 

The ID of the evaluation set item.

Example: `"evi_kR9mNP12Qw4yTv8BdR3H"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EvaluationSetItems.Update(EvaluationSetID, ItemID, request) -> *extend.EvaluationSetItem</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

If you need to change the expected output for a given evaluation set item, you can use this endpoint to update the item. This can be useful if you need to correct an error in the expected output or if the output of the extractor, classifier, or splitter has changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetItemsUpdateRequest{
        ExpectedOutput: &extend.ProvidedProcessorOutput{
            ProvidedExtractOutput: &extend.ProvidedExtractOutput{
                Value: &extend.JSONObject{
                    "invoice_number": "INV-001",
                    "total_amount": 1750,
                    "vendor_name": "Acme Corp",
                },
            },
        },
    }
client.EvaluationSetItems.Update(
        context.TODO(),
        "evaluation_set_id_here",
        "evaluation_set_item_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**evaluationSetID:** `string` 

The ID of the evaluation set.

Example: `"ev_2LcgeY_mp2T5yPaEuq5Lw"`
    
</dd>
</dl>

<dl>
<dd>

**itemID:** `string` 

The ID of the evaluation set item.

Example: `"evi_kR9mNP12Qw4yTv8BdR3H"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**expectedOutput:** `*extend.ProvidedProcessorOutput` — The expected output of the extractor, classifier, or splitter when run against the file. This must conform to the output schema of the entity associated with the evaluation set.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EvaluationSetItems.Delete(EvaluationSetID, ItemID) -> *extend.EvaluationSetItemsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete an evaluation set item.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetItemsDeleteRequest{}
client.EvaluationSetItems.Delete(
        context.TODO(),
        "evaluation_set_id_here",
        "evaluation_set_item_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**evaluationSetID:** `string` 

The ID of the evaluation set.

Example: `"ev_2LcgeY_mp2T5yPaEuq5Lw"`
    
</dd>
</dl>

<dl>
<dd>

**itemID:** `string` 

The ID of the evaluation set item.

Example: `"evi_kR9mNP12Qw4yTv8BdR3H"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EvaluationSetRuns
<details><summary><code>client.EvaluationSetRuns.Create(request) -> *extend.EvaluationSetRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create and start an async evaluation set run. The response returns the evaluation set run object with its initial status; use `GET /evaluation_set_runs/{id}` to poll for completion.

Evaluation set runs are currently supported for document processor evaluation sets.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetRunsCreateRequest{
        EvaluationSetID: "ev_2LcgeY_mp2T5yPaEuq5Lw",
        Entity: &extend.EvaluationSetRunsCreateRequestEntity{
            ID: "ex_Xj8mK2pL9nR4vT7qY5wZ",
            Version: extend.String(
                "1.0",
            ),
        },
    }
client.EvaluationSetRuns.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**evaluationSetID:** `string` — The ID of the evaluation set to run.
    
</dd>
</dl>

<dl>
<dd>

**entity:** `*extend.EvaluationSetRunsCreateRequestEntity` — Optional processor and version to run against the evaluation set. If omitted, the evaluation set's processor is run at its draft version.
    
</dd>
</dl>

<dl>
<dd>

**evaluationSetItemIDs:** `[]string` — Optional list of evaluation set item IDs to run. If omitted, all items in the evaluation set are run.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EvaluationSetRuns.Retrieve(ID) -> *extend.EvaluationSetRun</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of an evaluation set run.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.EvaluationSetRunsRetrieveRequest{}
client.EvaluationSetRuns.Retrieve(
        context.TODO(),
        "evaluation_set_run_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the evaluation set run.

Example: `"evr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## WebhookEndpoints
<details><summary><code>client.WebhookEndpoints.List() -> *extend.WebhookEndpointsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all webhook endpoints.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookEndpointsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.WebhookEndpoints.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `*extend.WebhookEndpointStatus` — Filter by endpoint status.
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebhookEndpoints.Create(request) -> *extend.WebhookEndpointCreate</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new webhook endpoint. The response includes a `signingSecret` that is only returned once — store it securely for verifying webhook signatures.

The `enabledEvents` array specifies which global event types this endpoint should receive. Use the [Webhook Events](https://docs.extend.ai/2026-02-09/developers/api-reference/webhook-events) reference to see available event types.

To subscribe to events scoped to a specific resource (e.g., a single extractor or workflow), use [Create Webhook Subscription](https://docs.extend.ai/2026-02-09/developers/api-reference/endpoints/webhook/create-webhook-subscription) after creating the endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookEndpointsCreateRequest{
        URL: "https://example.com/webhooks",
        Name: "Production webhook",
        EnabledEvents: []extend.WebhookEndpointEventType{
            extend.WebhookEndpointEventTypeExtractRunProcessed,
            extend.WebhookEndpointEventTypeWorkflowCreated,
        },
        APIVersion: "apiVersion",
    }
client.WebhookEndpoints.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**url:** `string` — The URL that webhook events will be sent to.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — A human-readable name for the webhook endpoint.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*extend.WebhookEndpointStatus` 
    
</dd>
</dl>

<dl>
<dd>

**enabledEvents:** `[]*extend.WebhookEndpointEventType` — The list of global event types to subscribe to. Pass an empty array to create an endpoint with no global events (useful if you only plan to use resource-scoped subscriptions).
    
</dd>
</dl>

<dl>
<dd>

**apiVersion:** `extend.APIVersionEnum` 
    
</dd>
</dl>

<dl>
<dd>

**advancedOptions:** `*extend.WebhookAdvancedOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebhookEndpoints.Retrieve(ID) -> *extend.WebhookEndpoint</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a webhook endpoint by ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookEndpointsRetrieveRequest{}
client.WebhookEndpoints.Retrieve(
        context.TODO(),
        "webhook_endpoint_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the webhook endpoint.

Example: `"wh_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebhookEndpoints.Update(ID, request) -> *extend.WebhookEndpoint</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update a webhook endpoint. Only the fields you include in the request body will be updated; omitted fields remain unchanged.

The `apiVersion` of a webhook endpoint cannot be changed after creation.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookEndpointsUpdateRequest{}
client.WebhookEndpoints.Update(
        context.TODO(),
        "webhook_endpoint_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the webhook endpoint to update.

Example: `"wh_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**url:** `*string` — The URL that webhook events will be sent to.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — A human-readable name for the webhook endpoint.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*extend.WebhookEndpointStatus` 
    
</dd>
</dl>

<dl>
<dd>

**enabledEvents:** `[]*extend.WebhookEndpointEventType` — The list of global event types to subscribe to.
    
</dd>
</dl>

<dl>
<dd>

**advancedOptions:** `*extend.WebhookAdvancedOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebhookEndpoints.Delete(ID) -> *extend.WebhookEndpointsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a webhook endpoint and all of its subscriptions. This operation is permanent and cannot be undone.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookEndpointsDeleteRequest{}
client.WebhookEndpoints.Delete(
        context.TODO(),
        "webhook_endpoint_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the webhook endpoint to delete.

Example: `"wh_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## WebhookSubscriptions
<details><summary><code>client.WebhookSubscriptions.List() -> *extend.WebhookSubscriptionsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List webhook subscriptions. You can filter by `webhookEndpointId` to see all subscriptions for a given endpoint, or by `resourceId` to see all subscriptions for a given resource.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookSubscriptionsListRequest{
        NextPageToken: extend.String(
            "xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ=",
        ),
    }
client.WebhookSubscriptions.List(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**webhookEndpointID:** `*string` — Filter subscriptions by the webhook endpoint they belong to.
    
</dd>
</dl>

<dl>
<dd>

**resourceID:** `*string` — Filter subscriptions by the resource they are scoped to.
    
</dd>
</dl>

<dl>
<dd>

**sortDir:** `*extend.SortDir` 
    
</dd>
</dl>

<dl>
<dd>

**nextPageToken:** `*extend.NextPageToken` 
    
</dd>
</dl>

<dl>
<dd>

**maxPageSize:** `*extend.MaxPageSize` 
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebhookSubscriptions.Create(request) -> *extend.WebhookSubscription</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a resource-scoped webhook subscription on an existing webhook endpoint.

Subscriptions let you receive events for a specific resource (e.g., a single extractor or workflow) rather than all resources of that type. The `enabledEvents` must be valid for the given `resourceType` and the endpoint's `apiVersion`.

If a subscription already exists for the same endpoint and resource, it will be updated with the new `enabledEvents` instead of creating a duplicate.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookSubscriptionsCreateRequest{
        WebhookEndpointID: "wh_Xj8mK2pL9nR4vT7qY5wZ",
        ResourceType: extend.WebhookSubscriptionResourceTypeExtractor,
        ResourceID: "ex_Xj8mK2pL9nR4vT7qY5wZ",
        EnabledEvents: []extend.WebhookSubscriptionEventType{
            extend.WebhookSubscriptionEventTypeExtractRunProcessed,
            extend.WebhookSubscriptionEventTypeExtractRunFailed,
        },
    }
client.WebhookSubscriptions.Create(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**webhookEndpointID:** `string` — The ID of the webhook endpoint to attach this subscription to.
    
</dd>
</dl>

<dl>
<dd>

**resourceType:** `*extend.WebhookSubscriptionResourceType` 
    
</dd>
</dl>

<dl>
<dd>

**resourceID:** `string` — The ID of the resource to scope this subscription to.
    
</dd>
</dl>

<dl>
<dd>

**enabledEvents:** `[]*extend.WebhookSubscriptionEventType` — The event types to subscribe to. Must be valid for the given `resourceType`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebhookSubscriptions.Retrieve(ID) -> *extend.WebhookSubscription</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a webhook subscription by ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookSubscriptionsRetrieveRequest{}
client.WebhookSubscriptions.Retrieve(
        context.TODO(),
        "webhook_subscription_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the webhook subscription.

Example: `"whes_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebhookSubscriptions.Update(ID, request) -> *extend.WebhookSubscription</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update the enabled events on a webhook subscription.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookSubscriptionsUpdateRequest{
        EnabledEvents: []extend.WebhookSubscriptionEventType{
            extend.WebhookSubscriptionEventTypeExtractRunProcessed,
        },
    }
client.WebhookSubscriptions.Update(
        context.TODO(),
        "webhook_subscription_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the webhook subscription to update.

Example: `"whes_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>

<dl>
<dd>

**enabledEvents:** `[]*extend.WebhookSubscriptionEventType` — The event types to subscribe to. Must be valid for the subscription's resource type.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebhookSubscriptions.Delete(ID) -> *extend.WebhookSubscriptionsDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a webhook subscription. This operation is permanent and cannot be undone.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &extend.WebhookSubscriptionsDeleteRequest{}
client.WebhookSubscriptions.Delete(
        context.TODO(),
        "webhook_subscription_id_here",
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 

The ID of the webhook subscription to delete.

Example: `"whes_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**extendWorkspaceID:** `*string` — The workspace ID to target. **Required** when using an organization-scoped API key; optional for workspace-scoped keys (the key is already tied to a workspace). See [Authentication](https://docs.extend.ai/2026-02-09/developers/authentication) for details on API key scopes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

