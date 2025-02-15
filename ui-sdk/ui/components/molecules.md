# Molecules

Complex components composed of multiple atoms, providing more sophisticated UI patterns for the Alquimia UI system.

## Layout Components

### PageContainer
Container component with standardized padding and max-width settings. Customizable with tailwind classes.
```tsx
<PageContainer className="px-[16px] md:px-[24px] lg:px-[120px]">
  <h1>Page Content</h1>
</PageContainer>
```

## Dialog Components

### AlertDialog
Modal dialog for important actions requiring user confirmation.
```tsx
  <AlertDialog>
    <AlertDialogTrigger>
      <Button>Open</Button>
    </AlertDialogTrigger>
    <AlertDialogContent>
      <AlertDialogHeader>
        <AlertDialogTitle>Are you absolutely sure?</AlertDialogTitle>
        <AlertDialogDescription>
          This action cannot be undone. This will permanently delete your
          account and remove your data from our servers.
        </AlertDialogDescription>
      </AlertDialogHeader>
      <AlertDialogFooter>
        <AlertDialogCancel>Cancel</AlertDialogCancel>
        <AlertDialogAction>Continue</AlertDialogAction>
      </AlertDialogFooter>
    </AlertDialogContent>
  </AlertDialog>
```

## Navigation Components

### NavigationMenu
Advanced navigation component with dropdown support.
```tsx
  <NavigationMenu>
    <NavigationMenuList>
      <NavigationMenuItem>
        <NavigationMenuTrigger>Menu</NavigationMenuTrigger>
        <NavigationMenuContent>
          <ul className="">
            <li className="row-span-3">
              <NavigationMenuLink asChild>
                <a
                  className=""
                  href="/"
                >
                  <div className="mb-2 mt-4 text-lg font-medium">
                    shadcn/ui
                  </div>
                  <p className="text-sm leading-tight text-muted-foreground">
                    Beautifully designed components that you can copy and
                    paste into your apps. Accessible. Customizable. Open
                    Source.
                  </p>
                </a>
              </NavigationMenuLink>
            </li>
            <ListItem href="/docs" title="Introduction">
              Re-usable components built using Radix UI and Tailwind CSS.
            </ListItem>
            <ListItem href="/docs/installation" title="Installation">
              How to install dependencies and structure your app.
            </ListItem>
            <ListItem href="/docs/primitives/typography" title="Typography">
              Styles for headings, paragraphs, lists...etc
            </ListItem>
          </ul>
        </NavigationMenuContent>
      </NavigationMenuItem>
      <NavigationMenuItem>
        <NavigationMenuTrigger>Components</NavigationMenuTrigger>
        <NavigationMenuContent>
          <ul className="grid w-[400px] gap-3 p-4 md:w-[500px] md:grid-cols-2 lg:w-[600px] ">
            {components.map((component) => (
              <ListItem
                key={component.title}
                title={component.title}
                href={component.href}
              >
                {component.description}
              </ListItem>
            ))}
          </ul>
        </NavigationMenuContent>
      </NavigationMenuItem>
      <NavigationMenuItem>
        <Link href="/docs" legacyBehavior passHref>
          <NavigationMenuLink className={navigationMenuTriggerStyle()}>
            Documentation
          </NavigationMenuLink>
        </Link>
      </NavigationMenuItem>
    </NavigationMenuList>
  </NavigationMenu>
```

### Sidebar
Configurable sidebar navigation component.
```tsx
const [selectedSection, setSelectedSection] = useState<SidebarItem>(
  sidebarItems[0]!
);
<Sidebar 
  items={[
    { name: "Dashboard", icon: HomeIcon },
    { name: "Settings", icon: SettingsIcon }
  ]}
  onSelect={(item) => setSelectedSection(item)}
  selectedSection={selectedSection}
/>
```

## Rating Components

### RatingStars
Star-based rating component. Receives a numeric rating as comment (0-5), and a function to handle the rating.
```tsx
 <RatingStars currentRating={rating} onRate={handleRate} isLoading={isLoading} />
```

### RatingThumbs
Thumbs up/down rating component. Receives a string rating as comment, and a function to handle the rating.
```tsx
    <RatingThumbs
      currentRating={rating}
      onRate={handleRate}
      isLoading={isLoading}
    />
```

### RatingComment
Text-based rating component with comment support. Receives a string rating as comment, and a function to handle the rating.
```tsx
  <RatingComment
    currentRating={comment}
    onRate={handleRate}
    isLoading={isLoading}
  />
```

## Display Components

### Carousel
Slideshow component for cycling through elements.
```tsx
  <Carousel className="w-full max-w-xs">
    <CarouselContent>
      {Array.from({ length: 5 }).map((_, index) => (
        <CarouselItem key={index}>
          <div className="p-1">
            Content
          </div>
        </CarouselItem>
      ))}
    </CarouselContent>
    <CarouselPrevious />
    <CarouselNext />
  </Carousel>
```

### CallOut
Highlighted information component. In this case, it's a chat message. The callout maps the messages to the role and the particular  message.
```tsx
  <CallOut key={index} role={message.role} message={message}>
    {messages.map((message, index) => (
      <CallOut key={index} role={message.role} message={message}>
        <div>
          <CallOutDate className="text-sm text-gray-500 mx-2 pb-1">
            {message.timestamp.toLocaleString("en-GB", {
              day: "2-digit",
              month: "2-digit",
              year: "numeric",
              hour: "2-digit",
              minute: "2-digit",
              second: "2-digit",
            })}
          </CallOutDate>
          <CallOutResponse role={message.role}>
            {message.content}
          </CallOutResponse>
          <CallOutActions actions={baseActions} role={message.role} />
        </div>
      </CallOut>
    ))}
  </CallOut>
```

## Interactive Components

### AssistantButton
Floating action button with hover-triggered suggestion menu. Commonly used for chat or help interfaces. Can be combined with the Drawer component to create a chat interface and trigger the drawer with the button, along with the suggestions.

```tsx
const messageSuggestions = [
  {
    label: "Help",
    icon: HelpCircle,
    action: () => handleSuggestion("What is this?"),
  },
  {
    label: "Features",
    icon: Target,
    action: () => handleSuggestion("Show me the features"),
  }
];

<AssistantButton
  icon={MessageCircle}
  clickAction={handleOpen}
  suggestions={messageSuggestions}
/>
```

Props:
- `icon`: LucideIcon component to display in the button
- `clickAction`: Function to execute on button click
- `className`: Optional custom classes
- `suggestions`: Array of suggestion objects with:
  - `label`: Text to display
  - `icon`: LucideIcon for the suggestion
  - `action`: Function to execute when suggestion is clicked

The component features a smooth animation when hovering, displaying a list of configurable suggestions that can trigger different actions.
