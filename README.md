## Hi there 👋

total_followers = 0
platform_counts = {}

for platform, svg_path in platforms.items():
    if not os.path.exists(svg_path):
        print(f"Warning: {svg_path} not found, skipping {platform}", file=sys.stderr)
        continue
    
    with open(svg_path, 'r') as f:
        svg_content = f.read()
    
    count_str = parse_follower_count(svg_content, platform)
    count_num = convert_to_number(count_str)
    
    platform_counts[platform] = {'str': count_str, 'num': count_num}
    total_followers += count_num
    
    print(f"{platform.capitalize()}: {count_str} ({count_num})", file=sys.stderr)

formatted_total = human_format(total_followers)
print(f"Total Followers: {formatted_total} ({total_followers})", file=sys.stderr)

# Output just the formatted total for use in other scripts
print(formatted_total)
return 0
    
   
