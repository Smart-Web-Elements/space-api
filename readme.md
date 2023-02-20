# (WIP)

# JetBrains Space API

[![GitHub issues](https://img.shields.io/github/issues/Smart-Web-Elements/space-api)](https://github.com/Smart-Web-Elements/space-api/issues)
[![Packagist Downloads](https://img.shields.io/packagist/dt/swe/space-api)](https://packagist.org/packages/swe/space-api)
[![Packagist Version](https://img.shields.io/packagist/v/swe/space-api)](https://packagist.org/packages/swe/space-api)
[![License](https://img.shields.io/packagist/l/swe/space-api)](https://packagist.org/packages/swe/space-api)
[![PHP Version](https://img.shields.io/packagist/php-v/swe/space-api)](https://packagist.org/packages/swe/space-api)

Simplify your PHP connection to [JetBrains Space](https://www.jetbrains.com/space/) with this package. It represents
the whole [Space HTTP API](https://www.jetbrains.com/help/space/api.html) and is always up-to-date (checks every day at
2am UTC for updates).

## Installation

Install this package with `composer require swe/space-api` and you're done. Don't forget to create an application in
your Space Organisation for the [client credentials flow](https://www.jetbrains.com/help/space/client-credentials.html)
and grand permissions. The (most) permissions for each request are included in the comments, like so:

```php
final class Blog extends AbstractApi
{
    /**
     * Permissions that may be checked: Article.View
     *
     * @param array $request
     * @param array $response
     * @return array
     * @throws GuzzleException
     */
    final public function getAllBlogPosts(array $request = [], array $response = []): array
    {
        $uri = 'blog';

        return $this->client->get($this->buildUrl($uri), $request, $response);
    }
}
```

## Examples:

```php
use Swe\SpaceAPI\HttpClient;
use Swe\SpaceAPI\Space;

$clientId = 'Your Client ID Here';
$clientSecret = 'Your Client Secret Here';
$url = 'Your Space URL';

$space = new Space(new HttpClient($url, $clientId, $clientSecret));

// Let's create a project.
$projectInformation = $space->projects()->createProject([
    'key' => [
        'key' => 'MY_PROJECT',
    ],
    'name' => 'My Project',
]);

// Create a new channel if not exist.
if ($space->chats()->channels()->isNameFree(['name' => 'General'])) {
    $channel = $space->chats()->channels()->addNewChannel([
        'name' => 'General',
        'description' => 'No specific topic..',
        'private' => false,
    ]);
}
```

## Information

All package classes are generated automatically.
The version will be the same as JetBrains Space (when versioning is included).
Please submit your issues on [GitHub](https://github.com/Smart-Web-Elements/space-api/issues).
