from datetime import date, timedelta


def calculate_reading_progress(total_pages, pages_read, pages_per_day):
    if total_pages <= 0:
        raise ValueError("Total pages must be positive")

    if pages_read < 0 or pages_read > total_pages:
        raise ValueError("Pages read must be between 0 and total pages")

    if pages_per_day <= 0:
        raise ValueError("Pages per day must be positive")

    remaining = total_pages - pages_read
    progress = pages_read / total_pages * 100
    days_left = (remaining + pages_per_day - 1) // pages_per_day
    completion_date = date.today() + timedelta(days=days_left)

    return {
        "total_pages": total_pages,
        "pages_read": pages_read,
        "pages_remaining": remaining,
        "progress_percent": round(progress, 2),
        "days_remaining": days_left,
        "estimated_completion": completion_date.isoformat(),
    }


if __name__ == "__main__":
    try:
        total = int(input("Total pages in the book: "))
        read = int(input("Pages already read: "))
        daily = int(input("Pages you read per day: "))

        result = calculate_reading_progress(total, read, daily)

        print("\nReading Progress")
        print("-" * 30)

        for key, value in result.items():
            print(f"{key.replace('_', ' ').title()}: {value}")

    except ValueError as error:
        print(f"Error: {error}")
