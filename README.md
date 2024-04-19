# How to solve cloudflare captcha | Solve cloudflare captcha

![](https://assets.capsolver.com/prod/images/post/2024-04-19/399c33d5-6b01-4b0b-9e78-93386181aea1.png)

Cloudflare CAPTCHA serves as a vital security measure to protect websites from automated bots and ensure a safe browsing experience for users. In this article, we will explore effective strategies to solve Cloudflare CAPTCHA challenges, while highlighting the capabilities of CapSolver, a leading automated CAPTCHA-solving solution.

## Bonus Code
 A bonus code for top captcha solutions; [CapSolver](https://www.capsolver.com/): **WEBS**. After redeeming it, you will get an extra 5% bonus after each recharge, Unlimited

![](https://assets.capsolver.com/prod/images/post/2024-03-29/fbc29472-886c-45b2-9eb2-2b307f6d9700.png)

## What is Cloudflare Captcha

Generally speaking, there are two different types of Cloudflare (Turnstile and Challenge 5S), but they both aim to distinguish between real people and bots for the purpose of website protection. Cloudflare Turnstile is a free tool that aims to replace CAPTCHAs. By implementing a simple snippet of code, Turnstile provides website visitors with a hassle-free browsing experience, free from CAPTCHA challenges. It effectively prevents abuse and verifies the authenticity of visitors without compromising data privacy or subjecting them to the unpleasant user experience associated with CAPTCHAs. With Turnstile, websites can offer a more seamless and enjoyable interaction for their users.Cloudflare Turnstile doesn't usually show the traditional interactive CAPTCHAs. Instead, it employs non-visual puzzles behind the scenes to verify real users and only shows a visible CAPTCHA box occasionally. Turnstile challenges are unpredictable, making it difficult for web scraper to overcome.


In terms of Challenge 5S, it uses the same underlying technology as Turnstile. It helps website owners to embed non-intrusive Cloudflare challenges on their websites to effectively prevent bot attacks. Also Cloudflare Challenge 5s introduces a brief 5-second delay before granting access to a website. Its purpose is to deter automated bots by requiring users to wait for a short period.

![](https://assets.capsolver.com/prod/images/post/2023-05-13/254a86e2-c054-4c42-9b57-5c219af2a3f8.gif)

## Why Cloudflare Deploys CAPTCHA

Cloudflare deploys CAPTCHA challenges as a defensive measure against malicious bots, safeguarding websites from unauthorized access, data breaches, and other cyber threats. However, these security measures can inadvertently cause inconvenience for legitimate users and developers who rely on automation for various tasks, such as data collection, testing, and monitoring.

## Challenges Faced by Web Scrapers
For web scrapers, the presence of CAPTCHA challenges poses a hurdle as it disrupts the automated data extraction process. Web scraping relies on efficiency and continuous data retrieval, and CAPTCHAs can introduce delays and interruptions. Web scrapers must find ways to overcome these challenges and adapt their scraping techniques to navigate CAPTCHA hurdles while maintaining the desired level of data accuracy and reliability.

To address the CAPTCHA challenges posed by Cloudflare, developers and web scraping practitioners explore various approaches. This includes implementing CAPTCHA-solving tools, such as [CapSolver](https://www.capsolver.com/), which leverages advanced automation techniques to tackle CAPTCHA challenges efficiently. CapSolver and similar solutions offer automation capabilities that can accurately solve CAPTCHAs, enabling web scrapers to proceed with their data extraction tasks seamlessly.


## How to solve cloudflare captcha

Here we'll take the example of solving Turnstile, which requires the use of CapSolver. In the beginning, there is no need to specify subtypes during your call. It is not necessary to provide your own custom `User-Agent` yet,
Lets  ignore this parameter.


The task type `type` is as follows

- `AntiTurnstileTaskProxyLess`

### Step 1 Create the task

Create the task with the [createTask](../api-createtask.md).

In the process of using turnstile, we must input `websiteURL` and `websiteKey`, other parameters are optional.

#### Task Object Structure

| Properties     | Type               | Required | Description                                                  |
| -------------- | ------------------ | -------- | ------------------------------------------------------------ |
| type           | String             | Required | `AntiTurnstileTaskProxyLess`                                 |
| websiteURL     | String             | Required | The address of the target page.                              |
| websiteKey     | String             | Required | Turnstile website key.                                       |
| metadata       | Map<String,String> | Required | Turnstile extra data . [Turnstile Documentation](https://developers.cloudflare.com/turnstile/get-started/client-side-rendering/) |
| metadata.acton | String             | Optional | The value of the `data-action` attribute of the Turnstile element if it exists. |
| metadata.cdata | String             | Optional | The value of the `data-cdata` attribute of the Turnstile element if it exists. |

#### **Example Request**

```txt
POST https://api.capsolver.com/createTask
Host: api.capsolver.com
Content-Type: application/json
```

```json lines
{
  "clientKey": "YOUR_API_KEY",
  "task": {
    "type": "AntiTurnstileTaskProxyLess",
    "websiteURL": "https://www.yourwebsite.com",
    "websiteKey": "0x4XXXXXXXXXXXXXXXXX",
    "metadata": {
       "action": "login",  //optional
       "cdata": "0000-1111-2222-3333-example-cdata"  //optional
    }
  }
}
```

#### Example Response

```json lines
{
  "errorId": 0,
  "status": "idle",
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"   // record taskId
}

```

### Step 2  **Getting Result**

Use the [getTaskResult](../api-gettaskresult.md) method to get the recognition results

Depending on the system load, you will get the results within the interval of `1s` to `20s`

#### **Example Request**

```txt
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json
```

```json lines
{
  "clientKey": "YOUR_API_KEY",
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"
}
```

#### Example Response

```json lines
{
  "errorId": 0,
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006",
  "status": "ready",
  "errorCode": null,
  "errorDescription": null,
  "solution": {
    "token": "0.mF74FV8wEufAWOdvOak_xFaVy3lqIDel7SwNhw3GgpICSWwTjYfrQB8mRT1dAJJBEoP7N1sESdp6WH9cTS1T0catWLecG3ayNcjwxVtr3hWfS-dmcBGRTx4xYwI64sAVboYGpIyuDBeMIRC3W8dK35v1nDism9xa595Da5VlXKM7hk7pIXg69lodfiftasIkyD_KUGkxBwxvrmz7dBo10-Y5zvro9hD4QKRjOx7DYj9sumnkyYCDx0m4ImDIIkNswfVTWI2V22wlnpHdvMgdtKYgOIIAU28y9gtdrdDkpkH0GHcDyd15sxQGd9VjwhGZA_mpusUKMsEoGgst2rJ3zA.UWfZupqLlGvlATkPo3wdaw.38d55cd0163610d8ce8c42fcff7b62d8981495cc1afacbb2f14e5a23682a4e13",
    "type": "turnstile",
    "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36"
  }
}
```

### Use SDK Request

::: code-group

```python
# pip install --upgrade capsolver
# export CAPSOLVER_API_KEY='...'

import capsolver

# capsolver.api_key = "..."
solution = capsolver.solve({
  "type": "AntiTurnstileTaskProxyLess",
  "websiteURL": "https://www.yourwebsite.com",
  "websiteKey": "0x4XXXXXXXXXXXXXXXXX",
  "metadata": {
	 "action": "login"  # optional
  }
})
```

```go [golang]
package main

import (
  "fmt"
  capsolver_go "github.com/capsolver/capsolver-go"
  "log"
)

func main() {
  // first you need to install sdk
  //go get github.com/capsolver/capsolver-go

  capSolver := capsolver_go.CapSolver{ApiKey: "..."}
  solution, err := capSolver.Solve(map[string]any{
    "type":       "AntiTurnstileTaskProxyLess",
    "websiteURL": "https://www.yourwebsite.com",
    "websiteKey": "0x4XXXXXXXXXXXXXXXXX",
    "metadata": map[string]string{
	  "action": "login"  // optional
    },
  })
  if err != nil {
    log.Fatal(err)
    return
  }
  fmt.Println(solution)
}

```

In conclusion, Cloudflare deploys CAPTCHA challenges as a security measure to protect websites from malicious bots and unauthorized access. While these challenges may pose obstacles for web scrapers, solutions like CapSolver can help automate the CAPTCHA-solving process, enabling efficient and reliable data extraction. Web scrapers must stay updated and adapt their strategies to navigate CAPTCHA challenges effectively and ensure the uninterrupted retrieval of valuable data.
